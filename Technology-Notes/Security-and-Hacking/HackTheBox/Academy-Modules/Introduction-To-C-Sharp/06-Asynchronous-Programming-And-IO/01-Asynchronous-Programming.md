`Asynchronous programming` is a powerful technique in modern software development that allows programs to `perform non-blocking operations` and efficiently utilise system resources. It enables applications to `handle time-consuming tasks without blocking the main execution thread`, improving responsiveness and scalability.

In traditional `synchronous programming`, when a method is invoked, the `program waits until the method completes` its execution before proceeding to the following line of code. This blocking behaviour can lead to poor performance and unresponsive applications, especially when dealing with I/O-bound or long-running operations. You can see this behaviour in applications when they appear to `freeze randomly` and `become unresponsive` when you try to load a large file, for instance. `Asynchronous programming` addresses this issue by `allowing tasks to execute independently` without blocking the main thread, enabling other `work to be done concurrently`.

To understand this concept better, it's important to distinguish between `concurrent` and `parallel` operations. `Concurrent` operations refer to tasks that `appear to occur simultaneously` but may not necessarily do so. On the other hand, `parallel` operations involve tasks that are `executed at the same time` on different cores or processors. Asynchronous programming primarily deals with `concurrent operations`, enabling multiple tasks to `progress independently of each other`.

Asynchronous methods return a `Task` or `Task<T>` object representing an ongoing operation. The calling code can continue its execution while the asynchronous operation progresses in the background. Once the operation completes, the result can be retrieved or further processed.

There are a few very important things to be aware of when utilising asynchronous programming:

- `Avoid Blocking Calls`: Use asynchronous versions of methods whenever possible to prevent blocking the main thread.
- `Configure async Methods Properly`: Ensure that `async` methods return `Task` or `Task<T>` and use the `await` keyword appropriately to await the completion of asynchronous operations.
- `Handle Exceptions`: Handle exceptions properly in asynchronous code. Use `try-catch` blocks to catch and handle exceptions that may occur during asynchronous operations. Unhandled exceptions can lead to unexpected application behaviour.
- `Use Cancellation Tokens`: Utilize cancellation tokens to allow the cancellation of asynchronous operations gracefully. This can improve the responsiveness and user experience of the application.

## async & await

In C#, asynchronous programming is facilitated by the `async` and `await` keywords.

The `async` keyword is used to specify that a method, lambda expression, or anonymous method is asynchronous. These methods usually return a `Task` or `Task<T>` object, representing ongoing work.

On the other hand, the `await` keyword is used in an `async` method to suspend the execution of the method until a particular task completes; the program is `awaiting Task<T>` completion. `await` can only be used in an `async` method.

The basic structure of an asynchronous method using `async` and `await` would look like this:

```csharp
async Task<T> MethodName()
{
    //...Method body
    await SomeTask;
    //...Continue after SomeTask finishes
}
```

- `async`: This keyword is used to specify that a method is asynchronous.
- `Task<T>`: An asynchronous method should return a `Task` or `Task<T>`. A `Task` represents an ongoing job that might not have been completed when your method returns. The job is executed concurrently with the rest of your program.
- `MethodName`: This is where you put the name of your method.
- Inside the method body, you use the `await` keyword before a task to specify that the method can't continue until the awaited task completes—meanwhile, control returns to the caller of the method.

```csharp
public async Task<int> CalculateSumAsync(int a, int b)
{
    await Task.Delay(500); //Simulate some delay
    return a + b;
}

public async void CallCalculateSumAsync()
{
    int result = await CalculateSumAsync(5, 6);
    Console.WriteLine($"The sum is {result}");
}
```

In this example, the method `CalculateSumAsync` is marked with the `async` keyword and returns a `Task<int>`. Inside the method, we simulate a delay with `Task.Delay`, which we `await`. This means that while we're waiting for the delay to finish, control can be given back to the caller of this method. After the delay is finished, we calculate the sum and return it. In `CallCalculateSumAsync`, we call our asynchronous method and immediately `await` its result. Once we have the result, we print it to the console.

Let's consider an example where we call a web service to fetch data. Fetching data from a web service can be time-consuming, so we will use `async` and `await` to ensure our application remains responsive during this operation.

```csharp
using System.Net.Http; // Network I/O is explained in more detail on the related page
using System.Threading.Tasks;

class Program
{
    static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        string responseBody = await GetWebsiteContentAsync("http://example.com");

        Console.WriteLine(responseBody);
    }

    static async Task<string> GetWebsiteContentAsync(string url)
    {
        HttpResponseMessage response = await client.GetAsync(url);
        response.EnsureSuccessStatusCode();
        string responseBody = await response.Content.ReadAsStringAsync();

        return responseBody;
    }
}
```

The `GetWebsiteContentAsync` method is responsible for fetching the content of a website. It uses an `HttpClient` to send an asynchronous GET request to the provided URL. The `await` keyword waits for the task to complete without blocking the rest of the code.

The `client.GetAsync` method returns a `Task<HttpResponseMessage>` representing the ongoing fetch operation. This task is awaited using the `await` keyword. After ensuring that the HTTP response status indicates success by calling the `EnsureSuccessStatusCode()` method, we read the content of the HTTP response message asynchronously using `response.Content.ReadAsStringAsync()`. This method returns a `Task<string>,` which is also awaited.

Finally, in our `Main` method, we call `GetWebsiteContentAsync` and await its result before writing it to the console.

## Tasks

A Task can be in one of three states: `created`, `running`, or `completed`. Once a Task is completed, it can either result in a value, an exception, or nothing at all.

There are two types of tasks: `Task` and `Task<T>`.

- A `Task` represents a single operation that does not return a value and usually executes asynchronously. After the operation is completed, the Task is marked as completed. This is essentially a `void` async method.
    
- `Task<T>` represents an asynchronous operation that returns a value. The value type (denoted by `T`) is known and can be retrieved once the Task has finished execution.
    

Creating tasks can be done using the `Task.Run` method or implement methods marked with the `async` keyword that return a `Task` or `Task<T>`. Here's an example of creating and running a task:

```csharp
Task<int> task = Task.Run(() => {
    // Simulate work.
    Thread.Sleep(1000);
    return 69;
});
```

In this example, we create a task that sleeps for one second to simulate work and then returns the integer 69.

## Task Cancellation

If necessary, tasks can also be cancelled through the use of cancellation tokens.

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
Task<int> task = Task.Run(() => {
    // Simulate work.
    Thread.Sleep(1000);
    cts.Token.ThrowIfCancellationRequested();
    return 42;
}, cts.Token);

// Cancel the task.
cts.Cancel();
```

`CancellationToken` is a struct that can be checked periodically by an operation, and if cancellation is requested, the operation can stop itself in a controlled manner.

Cancellation is signalled via the `CancellationTokenSource`. When you want to cancel one or more operations, you call `Cancel` on the `CancellationTokenSource`, which sends a signal to all linked `CancellationToken` instances.

```csharp
public async Task PerformOperationAsync(CancellationToken cancellationToken)
{
    for (int i = 0; i < 100; i++)
    {
        // Simulate some work.
        await Task.Delay(100);

        // Check for cancellation.
        cancellationToken.ThrowIfCancellationRequested();
    }
}

public async Task MainAsync()
{
    var cts = new CancellationTokenSource();

    var task = PerformOperationAsync(cts.Token);

    // After 500 ms, cancel the operation.
    await Task.Delay(500);
    cts.Cancel();

    try
    {
        await task;
    }
    catch (OperationCanceledException)
    {
        Console.WriteLine("Operation was cancelled.");
    }
}
```

In this example, we pass a `CancellationToken` to the `PerformOperationAsync` method. Inside the method, after each unit of work (simulated with `Task.Delay`), we check if cancellation has been requested using `cancellationToken.ThrowIfCancellationRequested()`. This method throws an `OperationCanceledException` if a cancellation has been requested.

In the `MainAsync` method, we start the operation and cancel it after 500 ms by calling `cts.Cancel()`. This sends a signal to the associated cancellation token. When we await the task, it throws an `OperationCanceledException`, which we catch and handle.

## Exception Handling with Async Code

Exception handling is a critical part of asynchronous programming. When you're dealing with asynchronous operations, there's always a possibility that something might go wrong. The operation could fail, the network could go down, data could be corrupted - the list goes on. Without proper exception handling, these errors could cause your application to crash or behave unpredictably.

Exceptions are propagated when you use `await` on the task. If the task has thrown any exceptions, `await` will re-throw that exception.

```csharp
try
{
    string result = await GetWebsiteContentAsync();
}
catch (HttpRequestException ex)
{
    Console.WriteLine($"An error occurred: {ex.Message}");
}
```

In this example, we make a web request using the fictitious `FetchDataFromWebAsync` method. If the request fails and throws an `HttpRequestException`, our `catch` block will handle it and write an error message to the console.

If you're dealing with multiple `Tasks` and want to handle exceptions for each Task independently, you can use `Task.ContinueWith`. This method creates a continuation that executes when the task completes, regardless of the state of the antecedent task.

```csharp
var task = FetchDataFromWebAsync();
task.ContinueWith(t =>
{
    if (t.IsFaulted)
    {
        Console.WriteLine($"An error occurred: {t.Exception.InnerException.Message}");
    }
});
```

In this example, `ContinueWith` is used to specify an action that will happen when the task completes. If the task is faulted (an unhandled exception was thrown), it writes an error message to the console.