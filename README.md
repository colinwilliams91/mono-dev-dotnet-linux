# How to run .net on Ubuntu 22.04

[mono-project documentation](https://www.mono-project.com/docs/getting-started/mono-basics/)

## Install
[mono-project installation instructions](https://www.mono-project.com/download/stable/#download-lin-ubuntu)

- Add the Mono repository to your system

**Ubuntu 20.04 will work with newer versions (_e.g. 22.04_)**
```
sudo apt install ca-certificates gnupg
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
```

- Install Mono

```
sudo apt install mono-devel[mono-project documentation](https://www.mono-project.com/docs/getting-started/mono-basics/)
```

[test if installation worked correctly here](https://www.mono-project.com/docs/getting-started/mono-basics/)
_this link also explains the contents of this repo_

## Repository Contents

#### Console Hello World
To test the most basic functionality available, copy the following code into a file called `hello.cs`

```
using System;

public class HelloWorld
{
    public static void Main(string[] args)
    {
        Console.WriteLine ("Hello Mono World");
    }
}
```

To compile, use csc:

    `csc hello.cs`

_Note: csc compiler is not available on all platforms or in very old Mono versions, in such cases use mcs instead._

The compiler will create “hello.exe”, which you can run using:

    `mono hello.exe`

The program should run and output:

"Hello Mono World"

#### HTTPS connections
To make sure HTTPS connections work, run the following command to check whether you can connect to nuget.org:

`csharp -e 'new System.Net.WebClient ().DownloadString ("https://www.nuget.org")'`

The program prints the website contents if everything works or throws an exception if it doesn’t.

#### WinForms Hello World
The following program tests writing a System.Windows.Forms application.

```
using System;
using System.Windows.Forms;

public class HelloWorld : Form
{
    static public void Main ()
    {
        Application.Run (new HelloWorld ());
    }

    public HelloWorld ()
    {
        Text = "Hello Mono World";
    }
}
```

To compile, use csc with the -r option to tell the compiler to pull in the WinForms libraries:

    `csc winform.cs -r:System.Windows.Forms.dll`

The compiler will create “hello.exe”, which you can run using:

    `mono winform.exe`

#### ASP.NET Hello World
Create a text file with the name hello.aspx and the content:

```
<%@ Page Language="C#" %>
<html>
<head>
   <title>Sample Calendar</title>
</head>
<asp:calendar showtitle="true" runat="server">
</asp:calendar>
```

Then run the xsp4 command from that directory:

`xsp4 --port 9000`

Use a web browser to contact http://localhost:9000/hello.aspx


