# Become familiar with the .NET development tools

# Setup Environment

## Visual Studio

### Prerequisites

- [Visual Studio 2019 version 16.6](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) or a later version with the .NET Core cross-platform development workload installed. The .NET Core 3.1 SDK is automatically installed when you select this workload.

For more information, see [Install the .NET Core SDK with Visual Studio](https://docs.microsoft.com/en-us/dotnet/core/install/windows#install-with-visual-studio).

## Create the app

Create a .NET Core console app project named "HelloWorld".

1. Start Visual Studio 2019.

2. On the start page, choose **Create a new project**.

![Create a new project button selected on the Visual Studio start page](https://docs.microsoft.com/en-us/dotnet/core/tutorials/media/with-visual-studio/start-window.png)

3. On the **Create a new project** page, enter **console** in the search box. Next, choose **C#** or Visual Basic from the language list, and then choose All platforms from the platform list. Choose the **Console App (.NET Core)** template, and then choose **Next**.

![Create a new project window with filters selected](https://docs.microsoft.com/en-us/dotnet/core/tutorials/media/with-visual-studio/create-new-project.png)

 >Tip
>
>If you don't see the .NET Core templates, you're probably missing the required workload. Under the **Not finding what you're looking for?** message, choose the **Install more tools** and features link. The Visual Studio Installer opens. Make sure you have the .NET Core cross-platform development workload installed.

4. In the Configure your new project dialog, enter **HelloWorld** in the **Project name** box. Then choose **Create**.

![Configure your new project window with Project name, location, and solution name fields](https://docs.microsoft.com/en-us/dotnet/core/tutorials/media/with-visual-studio/configure-new-project.png)

The template creates a simple "Hello World" application. It calls the [Console.WriteLine(String)](https://docs.microsoft.com/en-us/dotnet/api/system.console.writeline#System_Console_WriteLine_System_String_) method to display "Hello World!" in the console window.

The template code defines a class, `Program`, with a single method, Main, that takes a [String](https://docs.microsoft.com/en-us/dotnet/api/system.string) array as an argument:

```C#
//Copy
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

`Main` is the application entry point, the method that's called automatically by the runtime when it launches the application. Any command-line arguments supplied when the application is launched are available in the **`args`** array.

If the language you want to use is not shown, change the language selector at the top of the page.

## Run the app

Press **`Ctrl`+`F5`** to run the program without debugging.

A console window opens with the text "Hello World!" printed on the screen and some Visual Studio debug information.

![Console window showing Hello World Press any key to continue](https://docs.microsoft.com/en-us/dotnet/core/tutorials/media/with-visual-studio/hello-world-console.png)

2. Press any key to close the console window.

## Enhance the app

Enhance the application to prompt the user for their name and display it along with the date and time.

1. In Program.cs or Program.vb, replace the contents of the Main method, which is the line that calls `Console.WriteLine`, with the following code:

```C#
//Copy
Console.WriteLine("\nWhat is your name? ");
var name = Console.ReadLine();
var date = DateTime.Now;
Console.WriteLine($"\nHello, {name}, on {date:d} at {date:t}!");
Console.Write("\nPress any key to exit...");
Console.ReadKey(true);
```

This code displays a prompt in the console window and waits until the user enters a string followed by the `Enter` key. It stores this string in a variable named `name`. It also retrieves the value of the [DateTime.Now](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.now#System_DateTime_Now) property, which contains the current local time, and assigns it to a variable named date (`currentDate` in Visual Basic). And it displays these values in the console window. Finally, it displays a prompt in the console window and calls the [Console.ReadKey(Boolean)](https://docs.microsoft.com/en-us/dotnet/api/system.console.readkey#System_Console_ReadKey_System_Boolean_) method to wait for user input.

The `\n` (`vbCrLf` in Visual Basic) represents a newline character.

The dollar sign (`$`) in front of a string lets you put expressions such as variable names in curly braces in the string. The expression value is inserted into the string in place of the expression. This syntax is referred to as [interpolated strings](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated).

2. Press **`Ctrl`+`F5`** to run the program without debugging.

3. Respond to the prompt by entering a name and pressing the **`Enter`** key.

![Console window with modified program output](https://docs.microsoft.com/en-us/dotnet/core/tutorials/media/with-visual-studio/hello-world-update.png)

4. Press any key to close the console window.

[Docs](https://docs.microsoft.com/en-us/dotnet/core/tutorials/with-visual-studio)

## Visual Studio Code

The first step in running a tutorial on your machine is to set up a development environment. The .NET tutorial [Hello World in 10 minutes](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) has instructions for setting up your local development environment on Windows, Linux, or macOS.



Alternatively, you can install the [.NET Core SDK](https://dotnet.microsoft.com/download) and [Visual Studio Code](https://code.visualstudio.com/).

## Basic application development flow

You'll create applications using the [dotnet new](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new) command. This command generates the files and assets necessary for your application. The introduction to C# tutorials all use the console application type. Once you've got the basics, you can expand to other application types.

The other commands you'll use are [dotnet build](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-build) to build the executable, and [dotnet run](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-run) to run the executable.