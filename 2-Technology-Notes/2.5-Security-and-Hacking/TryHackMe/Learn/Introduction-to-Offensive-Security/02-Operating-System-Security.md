
## Task 1: Introduction to Operating System Security

Every day you use a smartphone or a laptop or almost any type of computer, you interact directly or indirectly with an operating system. Operating systems include MS Windows, macOS, iOS, Android, Chrome OS, and Linux. But what is an operating system? To define an operating system, we need to visit one computer term: hardware.

Computer hardware refers to all the computer parts and peripherals that you can touch with your hand. Hardware includes the screen, the keyboard, the printer, the USB flash memory, and the desktop board. As shown in the figure below, the desktop board contains many components, in particular, a central processing unit (CPU) and memory chips (RAM). Although not shown in the image below, the desktop board is usually connected to a storage device (HDD or SSD).

![[Hardware.png]]

The desktop board is the main part of a computer, and all the other pieces of hardware from keyboard and mouse to screen and printer connect to it. However, hardware components by themselves are useless if you want to run your favorite programs and applications. We need an Operating System to control and “drive” them.

![[Software.png]]

The Operating System (OS) is the layer sitting between the hardware and the applications and programs you are running. Example programs you would use daily might include a web browser, such as Firefox, Safari, and Chrome, and a messaging app, such as Signal, WhatsApp, and Telegram. All the programs and applications cannot run directly on the computer hardware; however, they run on top of the operating system. The operating system allows these programs to access the hardware according to specific rules.

Some operating systems are designed to run on laptops and personal desktops, such as MS Windows 11 and macOS. Other operating systems are designed specifically for smartphones, such as Android and iOS. There are also operating systems intended for servers; examples include [MS Windows Server 2022](https://www.microsoft.com/en-us/windows-server/), [IBM AIX](https://www.ibm.com/products/aix), and [Oracle Solaris](https://www.oracle.com/solaris). Finally, there are operating systems that you can use on a personal computer and server; one example is Linux. The image below shows the popularity of the different operating systems used to browse the Internet according to [Statcounter](https://gs.statcounter.com/os-market-share) based on the data collected during January 2022.

![[Operating-Systems.png]]

Your smartphone might be running Android or iOS, and you might have plenty of private data on it. Examples include:

1. Private conversations with your family and friends
2. Private photos with family and friends
3. Email client that you use for personal and work communications
4. Passwords saved in the web browser (or even in notes)
5. E-banking apps

The list of confidential and private data goes on. You don’t want someone you don’t trust to open your phone and go through your photos, conversations, and apps. Hence, you need to secure your phone and its operating system.

The same goes for your laptop or computer running MS Windows, macOS, or Linux. Your computer will most likely contain plenty of information such as:

1. Confidential files related to your work or university
2. Private personal files, such as a copy of your ID or passport
3. Email programs, such as MS Outlook and Mozilla Thunderbird
4. Passwords saved in web browsers and other apps
5. Copy of digital camera and smartphone photos

The list can get very long, depending on the type of user. And considering the nature of the saved data, you want to ensure that your data is secure. When we talk about security, we should think of protecting three things:

- Confidentiality: You want to ensure that secret and private files and information are only available to intended persons.
- Integrity: It is crucial that no one can tamper with the files stored on your system or while being transferred on the network.
- Availability: You want your laptop or smartphone to be available to use anytime you decide to use it.

![[CIA.png]]

<br>

---

<br>

## Task 2: Common Examples of OS Security

As we mentioned in the previous task, security is concerned with attacks against:

1. Confidentiality
2. Integrity
3. Availability

In this room, we will focus on three weaknesses targeted by malicious users:  

1. Authentication and Weak Passwords
2. Weak File Permissions
3. Malicious Programs

### Authentication and Weak Passwords

Authentication is the act of verifying your identity, be it a local or a remote system. Authentication can be achieved via three main ways:

- Something you know, such as a password or a PIN code.
- Something you are, such as a fingerprint.
- Something you have, such as a phone number via which you can receive an SMS message.

Since passwords are the most common form of authentication, they are also the most attacked. Many users tend to use easy-to-guess passwords or the same password on many websites. Moreover, some users rely on personal details such as date of birth and name of their pet, thinking that this is easy to remember and unknown to attackers. However, attackers are aware of this tendency among users.

The National Cyber Security Centre (NCSC) has published a list of the [100,000 most common passwords](https://www.ncsc.gov.uk/blog-post/passwords-passwords-everywhere). Let’s look at the top 20 passwords in the table below.

|Rank|Password|
|---|---|
|1|123456|
|2|123456789|
|3|qwerty|
|4|password|
|5|111111|
|6|12345678|
|7|abc123|
|8|1234567|
|9|password1|
|10|12345|
|11|1234567890|
|12|123123|
|13|000000|
|14|iloveyou|
|15|1234|
|16|1q2w3e4r5t|
|17|qwertyuiop|
|18|123|
|19|monkey|
|20|dragon|

We can see that 123, 1234, 12345, …, 123456789, and 1234567890 are on the list. Dictionary words such as password, iloveyou, monkey, and dragon are commonly used. Words not in the dictionary include qwerty, qwertyuiop, and 1q2w3e4r5t; these seemingly complex passwords are very predictable as they follow the keyboard layout.

In brief, if the attacker can guess the password of any of your online accounts, such as your email or social media account, they will be able to gain access to your private data. Therefore, it is vital that you choose complex passwords and use different passwords with different accounts.

### Weak File Permissions

Proper security dictates the principle of least privilege. In a work environment, you want any file accessible only by those who need to access it to get work done. On a personal level, if you are planning a trip with family or friends, you might want to share all the files related to the trip plan with those going on that trip; you don’t want to share such files publicly. That’s the principle of least privilege, or in simpler terms, “who can access what?”

Weak file permissions make it easy for the adversary to attack confidentiality and integrity. They can attack confidentiality as weak permissions allow them to access files they should not be able to access. Moreover, they can attack integrity as they might modify files that they should not be able to edit.

### Access to Malicious Programs

The last example we will consider is the case of malicious programs. Depending on the type of malicious program, it can attack confidentiality, integrity, and availability.

Some types of malicious programs, such as Trojan horses, give the attacker access to your system. Consequently, the attacker would be able to read your files or even modify them.

Some types of malicious programs attack availability. One such example is ransomware. Ransomware is a malicious program that encrypts the user's files. Encryption makes the file(s) unreadable without knowing the encryption password; in other words, the files become gibberish without decryption (reversing the encryption). The attacker offers the user the ability to restore availability, i.e., regain access to their original files: they would give them the encryption password if the user is willing to pay the “ransom.”

<br>

---

<br>

## Task 3: Practical Example of OS Security

In one typical attack, the attacker seeks to gain access to a remote system. We can accomplish this attack by tricking the target into running a malicious file or by obtaining a username and a password. We will focus on the latter. After discovering a username, we will try to “guess” the password; furthermore, we will try to escalate our privileges to a system administrator. This account is called `root` on Android, Apple, and Linux systems. While, on MS Windows systems, this account is called `administrator`. The accounts `root` and `administrator` have complete unrestricted access to a system.

In this task, we will try to hack into a Linux system. We assume that you have never used a Linux system before, and we will explain accordingly.

Start the AttackBox by clicking on the blue “Start AttackBox” button at the top right of the room. Start the attached machine by clicking on the green “Start Machine” button at the top right of this task. It usually takes a minute or two to load fully. Once they are both ready, you should use the AttackBox, which should be taking the right half of your screen by now.

![[Open-Terminal.png]]

On the AttackBox, start the terminal by clicking on the terminal icon shown in the image above. You will be writing all the commands you need on the terminal shown below.

![[Terminal-Application.png]]

We will cover the following Linux commands and explain them throughout this task.

- `whoami`
- `ssh USERNAME@MACHINE_IP`
- `ls`
- `cat FILENAME`
- `history`

We were hired to check the security of a certain company. When we visited our client’s office, we noticed a sticky note with two words: `sammie` and `dragon` on one of the screens. Let’s see if `dragon` is Sammie’s password on the target machine `MACHINE_IP`. From the AttackBox’s terminal, we will try to log in to Sammie’s account by executing `ssh sammie@MACHINE_IP`. The remote system will ask you to provide `sammie`’s password, `dragon`.

The first time we connect to a server over SSH, we will get a warning about the server’s authenticity and SSH key. We need to answer “Are you sure you want to continue connecting (yes/no)?” with yes.

Please note the following when entering the password over SSH. When you log in via SSH, you won't see that you are typing the password. In other words, **when you are typing the SSH password, you won't see stars, dots, or any indicator on the screen that the password is being typed**. However, the system still receives the password you are entering.

The interaction on the AttackBox’s terminal is shown below.

![[AttackBox-Terminal-1.png]]

Amazing! It worked! Let’s confirm that we are logged in as Sammie using the `whoami` (_who am I?_) command, which should return `sammie`.

To list the files in the current directory, we can use `ls`, short for _list_. This command will show all the files in the current directory unless they are hidden.

If you want to display the contents of any text file, you can use the command `cat FILENAME`, short for _concatenate_. This command will print the contents of the file on the screen.

In the terminal below, we see the usage of the four commands: `ssh`, `whoami`, `ls`, and `cat`. Please follow along from the AttackBox’s terminal.

![[AttackBox-Terminal-2.png]]

In our brief introduction to Linux, the last command that we will cover is `history`. This command prints the commands used by the user.

We have learned about two other usernames that can access the attached machine. They are:

- `johnny`
- `linda`

We know that both of these users have little regard for cybersecurity best practices. We can use several ways to guess the passwords for these two users. Here we list two approaches:

- If you are **not** logged in as `sammie` or any other user, you can use `ssh johnny@MACHINE_IP` and manually try one password after the next to see which password works for `johnny`.
- If you are logged in as `sammie` or any other user, you can use `su - johnny` and manually try one password after the next to see which password works for `johnny`.