# learn-asp.net-core-MVC-.net-8
My notes about asp.net core MVC [.net 8]

# Video Course
https://www.youtube.com/watch?v=AopeJjkcRvU&t=909s

# Microsoft Official Guide
* https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0&tabs=visual-studio
* https://learn.microsoft.com/it-it/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0&tabs=visual-studio

# Project Resources
* https://github.com/bhrugen/Bulky_MVC/tree/15a896555835fae1482fb1536e549dc132c92249

# Notes
## Topic
* [Fundamentals of ASP.NET Core](#Fundamentals-of-ASP.NET-Core)
* [Prerequisites](#Prerequisites)
* [Tools Needed](#Tools-Needed)
* [Welcome project](#Welcome-project)
* MVC Application
* Client and Server Validation
* Entity Framework Core And Repository Pattern
* DataTable / Toastr / File Uploads / RichText Editor
* Razor Pages
* ERROR SOLVING
## Fundamentals of ASP.NET Core 
* Fast
* Open Source
* Cross-platform
* Built-in dependency injection
* easy updates
* cloud-friendly
* Performance
## Prerequisites
* C# Basics
* SQL Basics 
## Tools Needed
* [Install .net8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
* Visual Studio Code
* SSMS 2018 (for database and sql server and management)
## Welcome project
### Create a project and execute it
To create .net project firstly you open a window in VS code. In the explorer page click "Create .net project". Now the search bar is enabled and in this case, you digit the "MVC" and at this moment appear "asp.net core mvc App..." and you click this entry.
As a result, you choose the folder project and afterward, you can set the name project. At this moment there are a lot of files, but for the first project you can click "Program.cs". You execute the program without a debugger. The consequence is the opening of the browser and on display will appear.
![welcomeImg](https://github.com/SimoneMoreWare/learn-asp.net-core-MVC-.net-8-/blob/main/img/welcome.png)
### file with .csproj exstension
The file with extension .csproj contains this:
```
xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

</Project>
```
These parameters are found within an ASP.NET Core project file (likely a .csproj file) and define some key settings of the project.
* `<Project Sdk="Microsoft.NET.Sdk.Web">`: This line specifies which SDK is used to build the project. In this case, the Microsoft.NET.Sdk.Web SDK is used, which is specific for ASP.NET Core web application development.
* `<PropertyGroup>`: This is an XML element containing a group of project properties. Within this element, project settings are specified.
* `<TargetFramework>net8.0</TargetFramework>`: This indicates the target framework version for the project. In this specific case, the project targets the .NET 8.0 framework. This framework defines the available APIs and libraries for the application.
* `<Nullable>enable</Nullable>`: This setting enables support for nullable reference types in the project. This allows the compiler to detect and report potential null reference issues during compilation.
* `<ImplicitUsings>enable</ImplicitUsings>`: This enables implicit namespace usage within the project. This means that common namespaces such as System, System.Collections.Generic, etc., do not need to be explicitly specified. The compiler will include them automatically.
### launchSettings.json
On the other hand,  launchSettings.json contains
```
json
{
  "$schema": "http://json.schemastore.org/launchsettings.json",
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:54996",
      "sslPort": 44332
    }
  },
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5207",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:7121;http://localhost:5207",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```
This block of code represents the launchSettings.json file used in ASP.NET Core projects to configure application startup settings. Here's an explanation:

* The $schema line specifies the JSON schema used for the configuration file. In this case, the file follows the schema defined at the specified URL.
* The iisSettings section defines specific settings for IIS Express, a local web server used for development. It specifies whether Windows authentication is disabled, anonymous authentication is enabled and provides details about the application URL and SSL port.
* The profiles section defines various launch profiles for the application. It includes profiles for launching with HTTP and HTTPS, as well as using IIS Express. Each profile has different settings such as the command name, whether to show dotnet run messages, whether to automatically open the browser, the application URL, and environment variables.
* The last part is an example profile for launching using IIS Express. It specifies the command to execute, whether to automatically launch the browser, and environment variables to set, such as the ASP.NET Core environment.
  * In ASP.NET Core, the `ASPNETCORE_ENVIRONMENT` environment variable is used to specify the environment in which the application is running. This environment variable can have different values such as `Development`, `Staging`, or `Production`, and it influences various aspects of the application's behavior, such as logging levels, error handling, and configuration settings.
  * Setting `ASPNETCORE_ENVIRONMENT` to `"Development"` in this launch profile indicates that the application should run in the development environment. This typically means that the application will use development-specific settings and configurations, which can be helpful during the development and debugging process.
### wwwroot folder
However, the wwwroot folder is important in the application. This folder will host all of the static content (CSS, JS, nuget packages or third-party libraries, image, PDF, PowerPoint ecc..) of your .net core of your project (in static content there isn't html code).
### appsettings.json
In other ways, the appsettings.json file in an ASP.NET Core application is a JSON formatted file that stores configuration data. In this file, you can keep settings like connection strings, application settings, logging configuration, and anything else you want to change without recompiling your application. The settings in this file can be read at runtime and overridden by environment-specific files like appsettings.Development.json or appsettings.Production.json.


