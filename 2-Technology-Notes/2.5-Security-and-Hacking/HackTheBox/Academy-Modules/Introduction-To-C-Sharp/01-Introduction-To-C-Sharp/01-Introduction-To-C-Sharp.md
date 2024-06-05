`C#` (pronounced "C sharp") is a general-purpose, object-oriented programming (OOP) language developed by Microsoft within its `.NET` initiative. It is fundamentally rooted in the C and C++ family of languages and borrows aspects from Java, making C# very familiar for developers of those languages.

- Hello world in C#

```csharp
using System;
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```

- Hello world in C++

```cpp
#include <iostream>
int main()
{
    std::cout << "Hello, World!";
    return 0;
}
```

- Hello world in Java

```java
public class Main
{
    public static void main(String[] args)
    {
        System.out.println("Hello, World!");
    }
}
```

The C# project commenced in the late 1990s, known initially as `Cool`, an acronym for "C-like Object Oriented Language". The driving force for the project was to build a language that offered the computational power of C++ combined with the simplicity of Visual Basic. Its key designer was Anders Hejlsberg, a prominent engineer previously involved in designing Turbo Pascal and Delphi at Borland, who still serves as the lead architect of C#.

C# was officially announced in July 2000, with the release of .NET Framework 1.0 following in 2002. C# is one of several languages that can be used to build .NET applications but by far the most dominant. Other languages can be used with the .NET Framework, such as Visual Basic and F#.

The `.NET Framework` is a language-agnostic software development and runtime platform developed by Microsoft. It provides a controlled environment for developing and running applications. Programs written for the .NET Framework execute in a software environment known as the `Common Language Runtime` (CLR), an application virtual machine that provides services such as security, memory management, and exception handling. There are many different components to the .NET Framework; some are listed below:

- The `Common Language Runtime (CLR)` is the execution engine for .NET Framework applications. It provides various services, such as memory management and thread management.
- The `.NET Framework Class Library (FCL)` is a standard library that encapsulates many common functions, such as file reading and writing, graphic rendering, database interaction, and XML document manipulation.
- `Common Language Specification (CLS)` is a set of rules and standards that enforce language interoperability.
- `Common Type System (CTS)` is a standard that defines all possible data types and programming constructs supported by CLR and how they interact.

### JIT

Just-In-Time compilation, or `JIT`, is a significant component of runtime environments in many modern programming languages, such as Java, Python with PyPy, LUA with LuaJIT and the .NET languages like C#. Programming Languages broadly fall into two categories: `Interpreted languages` and `compiled languages`, and a JIT compiler straddles the divide between the two.

A `statically compiled` language compiles (translates) the source code to machine code before execution. In this machine code format, the compiled binary represents the instruction set that a CPU interprets and executes. This approach offers more optimised performance than interpretation because the translation is done beforehand. However, static compilation requires additional development time due to the compile-link-execute cycle, and the resulting binaries are platform-specific.

In contrast, source code is not directly translated to machine code in an `interpreted language`. Instead, a separate program called the interpreter reads and executes the source code instructions. While this simplifies the development process because no compilation and linking steps are necessary, it can lead to slower execution speed because the interpretation needs to be performed as the program runs.

Just-In-Time compilation aims to combine the benefits of both `interpretation` and `static compilation`. It translates the source code into an intermediate form, akin to bytecode, a portable, platform-independent code. The bytecode is closer to machine code than the high-level source code but is not tied to a specific hardware configuration.

The bytecode is translated to machine code when the program is executed, but not in one big chunk. Instead, the translation happens just in time (hence the name), i.e., right before each portion of the code is executed. This strategy of deferred compilation aims to avoid the overhead of compiling parts of the program that are never executed during a particular run.

A JIT compiler is part of the `Common Language Runtime` (`CLR`). Instead of building machine code during compilation, .NET compiles into an intermediate language called the Microsoft Common Intermediate Language (MSIL or CIL). The processor then executes this machine code. The CLR maintains a cache of compiled methods during the program's execution. If a method is called more than once, the CLR can skip the JIT compilation step on subsequent calls and use the previously compiled machine code, resulting in performance improvements.

It's worth noting that there is a trade-off in JIT compilation between startup time and execution speed. JIT compilation can slow program start-up because the initial compilation to machine code happens during runtime. However, once the program runs, execution can be very fast—often comparable to statically compiled code.

### .NET Core and .NET

Microsoft introduced `.NET Core` as a successor to the .NET Framework, addressing many of the limitations and concerns with the .NET Framework, such as it is Windows-specific and not compatible with other platforms. .NET Core is a cross-platform framework designed for building modern, cloud-based, and internet-connected applications. It runs on Windows, Linux, and macOS, making it a suitable choice for developers aiming for wide compatibility. .NET Core comprises `CoreCLR`, a complete runtime, and `CoreFX`, a library built to run apps. It was first released in June 2016.

In 2020, Microsoft announced it was consolidating its .NET offerings into a single .NET platform. This marked the birth of `.NET 5`, which aimed to unify the .NET Framework and .NET Core. The unification process was designed to take the best from .NET Core, .NET Framework, Xamarin, and Mono to build a single platform for all .NET applications. The shift aimed to provide a single .NET runtime and framework that can be used everywhere, further strengthening the .NET platform's versatility and robustness.

The advent of .NET 5 and its successors (.NET 6, 7, 8 and beyond) has ushered in an era where developers no longer have to pick and choose different .NET technologies for different types of applications. Instead, they can use a unified platform for all their work, reducing the complexity of building and deploying .NET applications.

One of the key features of .NET 5 and later versions is their support for a broad spectrum of application types, including web applications, desktop applications, cloud services, IoT applications, machine learning, and more.

Furthermore, .NET 5 and its successors follow a `release schedule` with updates every November. Microsoft has committed to long-term support (LTS) releases every two years, ensuring stability and support for developers who prefer not to update their .NET runtime and libraries annually.

## What is C# used for

C# is a versatile and powerful programming language that can be employed to construct various program types to fulfil diverse needs and requirements. Here is a snapshot of the broad range of applications you can build with C#:

1. `Console Applications`: Perfect for building command-line interfaces, these applications are text-driven, devoid of graphical user interfaces (GUIs), and ideal for crafting simple utilities or scripts.
2. `Windows Forms Applications (WinForms)`: These GUI desktop applications come packed with a rich set of controls, including text boxes, labels, and buttons.
3. `Windows Presentation Foundation (WPF) Applications`: WPF offers a framework for creating sophisticated desktop applications with advanced UI features such as graphics, multimedia, and animations.
4. `Universal Windows Platform (UWP) Applications`: UWP apps are designed to provide a universal experience across Windows 10, Windows 10 Mobile, Windows 11, Xbox One, Xbox Series X/S, and HoloLens.
5. `Xamarin Applications`: Xamarin provides a platform for crafting mobile applications operable on multiple platforms, including iOS, Android, and Windows, all from a unified C# codebase.
6. `.NET Multi-platform App UI (MAUI) Applications`: MAUI is the evolution of `Xamarin`, extending from mobile to desktop. It allows for creating cross-platform Android, iOS, macOS, and Windows applications with a single codebase. Using MAUI, developers can create flexible and high-performance native applications using .NET and C#.
7. `ASP.NET Applications`: ASP.NET is a robust framework for building dynamic web applications, capable of serving web pages, RESTful APIs, real-time services, and more.
8. `Web Services`: These applications, accessible over standard web protocols like HTTP, SOAP, and REST, facilitate communication between applications over the Internet.
9. `Class Libraries`: These encompass collections of classes and other types that can be utilised by different applications, supporting code reuse and modular design.
10. `Unity Games`: Unity is a widely-used game development platform, with C# employed for scripting game behaviour.

## Installing the DevEnv

Visual Studio and Visual Studio Code are the most common IDEs for C# development. This module will use Visual Studio Code but feel free to use Visual Studio if you are on Windows. Install the `.NET Desktop Developer` meta package from the Visual Studio installer if you choose to go that route; otherwise, follow the instructions below.

![[Install.webp]]

### VSCode

1. Navigate to the Visual Studio Code download page at the following URL: https://code.visualstudio.com/Download
2. Download the version suitable for your operating system (Windows, macOS, or Linux).
3. Run the downloaded installer.
4. Follow the instructions in the installer.

### .NET

There are a few ways to install `.NET`. Regardless of how or what platform you install `.NET` onto, you can validate your installation by running `dotnet --version` from a terminal window.

Introduction to C#

```powershell-session
C:\> dotnet --version

7.0.304
```

This command will output the version of .NET installed on your machine. If you see the version number of the version you installed, then the installation was successful.

|Operating System|Installation|
|:--|:--|
|Windows|The easiest method to install `.NET` onto Windows is via the `winget` package manager. You can refer to the [Microsoft installation documentation for Windows](https://learn.microsoft.com/en-us/dotnet/core/install/windows) for other installation methods.|
|Linux|Most Linux distributions provide official versions of `.NET`. Check your package manager for install instructions or refer to the [Microsoft installation documentation for Linux](https://learn.microsoft.com/en-us/dotnet/core/install/linux) for other installation methods.|
|macOS|You can either install via the installer downloading from the `.NET Website` or install via `homebrew`. Refer to the [Microsoft installation documentation for macOS](https://learn.microsoft.com/en-us/dotnet/core/install/macos)|

C# can also be utilised in a manner similar to interpreted languages, like Python, with tools such as [LINQPad](https://www.linqpad.net/) or [CSharpRepl](https://github.com/waf/CSharpRepl). Furthermore, extensions are available that enable a Jupyter-like [notebook experience in VSCode](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode) or a kernel extension to [use .NET in Jupyter](https://github.com/dotnet/interactive/blob/main/docs/NotebookswithJupyter.md) directly.

### PwnBox

PwnBox, fully usable in this module, comes with VSCodium, a fork of VSCode pre-installed. Due to licensing constraints, VSCodium lacks the Microsoft extensions like the `C#` extension. Although a possible alternative exists on the OpenVSX registry—since VSCodium can't utilise the Microsoft VSX registry— we suggest installing VSCode per the instructions above to access the Microsoft `C#` extension.

If VSCode does not appear in any shortcut menus after installing the package, you can launch it from the terminal via `code`. Search and install for the `C#` extension if it is not installed.

![[Visual-Studio-Code.webp]]

As it stands at the time of writing, PwnBox comes pre-installed with .NET Core 3.1 and .NET 6. You're welcome to use .NET 6, or if you prefer, you can install .NET 7 by following the above instructions.

#### PwnBox dotnet info

```shell-session
user@htb[/htb]$ dotnet --info

.NET SDK (reflecting any global.json):
 Version:   6.0.408
 Commit:    0c3669d367

Runtime Environment:
 OS Name:     parrot
 OS Version:  5.3
 OS Platform: Linux
 RID:         linux-x64
 Base Path:   /usr/share/dotnet/sdk/6.0.408/

global.json file:
  Not found

Host:
  Version:      6.0.16
  Architecture: x64
  Commit:       1e620a42e7

.NET SDKs installed:
  3.1.426 [/usr/share/dotnet/sdk]
  6.0.408 [/usr/share/dotnet/sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.App 3.1.32 [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 6.0.16 [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 3.1.32 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
  Microsoft.NETCore.App 6.0.16 [/usr/share/dotnet/shared/Microsoft.NETCore.App]

Download .NET:
  https://aka.ms/dotnet-download

Learn about .NET Runtimes and SDKs:
  https://aka.ms/dotnet/runtimes-sdk-info
```

### .NET CLI

We will interact with `dotnet` via a console more than anything, as Visual Studio Code does not have the same level of 'hands-off tooling' that a full IDE, such as Visual Studio, provides. Below is a breakdown of some of the important commands to know:

- `dotnet new`: Creates a new .NET project. You can specify the type of project (`console`, `classlib`, `webapi`, `mvc`, etc.). For example, `dotnet new console` will create a new console application.
- `dotnet build`: Builds a .NET project and all of its dependencies. The `-c` or `--configuration` option can be used to specify the build configuration (`Debug` or `Release`).
- `dotnet run`: Builds and runs the .NET project. It is typically used during the development process to run the application for testing or debugging purposes.
- `dotnet test`: Runs unit tests in a .NET project using a test framework such as `MSTest`, `NUnit`, or `xUnit`.
- `dotnet publish`: Packs the application and its dependencies into a folder for deployment to a hosting system. The `-r` or `--runtime` option can be used to specify the target runtime.
- `dotnet add package`: Adds a NuGet package reference to the project file. You specify the package by name. For example, `dotnet add package Newtonsoft.Json`.
- `dotnet remove package`: Removes a NuGet package reference from the project file. Similar to the `add package` command, you specify the package to remove by name.
- `dotnet restore`: Restores the dependencies and tools of a project. This command is implicitly run when you run `dotnet new`, `dotnet build`, `dotnet run`, `dotnet test`, `dotnet publish`, and `dotnet pack`.
- `dotnet clean`: Cleans the output of a project. This command is typically used before you build the project again, as it deletes all the previously compiled files, ensuring that you start from a clean state.
- `dotnet --info`: Displays detailed information about the installed .NET environment, including installed versions and all runtime environments.

### A template quirk

We will use the Console template for running all code in this module; however, beginning with .NET 6, the template for creating new C# console applications (`dotnet new console`) generates the following template:

```csharp
// Refer to https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

This output utilises recent C# features that reduce the amount of code required for a straightforward program. This approach is suitable for small-scale projects operating entirely without a specific structure. However, for our purposes, this project style won't be suitable. Instead, it's recommended to use the provided template for projects.

```csharp
class Program
{
    public static void Main()
    {
        // ...
    }
}
```