# learn-asp.net-core-MVC-.net-8
My notes about asp.net core MVC [.net 8]

# Video Course
* https://www.youtube.com/watch?v=AopeJjkcRvU&t=909s
* https://www.youtube.com/watch?v=BzlPrVB_DwA
* https://www.youtube.com/watch?v=BzlPrVB_DwA&t=5177s

# Microsoft Official Guide
* https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0&tabs=visual-studio
* https://learn.microsoft.com/it-it/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0&tabs=visual-studio

# Sites
* https://dotnettutorials.net/lesson/viewimports-in-asp-net-core-mvc/#google_vignette
* https://www.tutorialsteacher.com/core/aspnet-core-program
* https://www.c-sharpcorner.com/article/full-stack-web-development-in-asp-net-core-8-mvc/

# Project Resources
* https://github.com/bhrugen/Bulky_MVC/tree/15a896555835fae1482fb1536e549dc132c92249

# Notes
## Topic
* [Fundamentals of ASP.NET Core](#Fundamentals-of-ASP.NET-Core)
* [Prerequisites](#Prerequisites)
* [Tools Needed](#Tools-Needed)
* [Welcome project](#Welcome-project)
    * [Create a project and execute it](#Create-a-project-and-execute-it)
    * [file with .csproj exstension](#file-with-.csproj-exstension)
    * [launchSettings.json](#launchSettings.json)
    * [wwwroot folder](#wwwroot-folder)
    * [appsettings.json](#appsettings.json)
    * [program.cs](#program.cs)
    * [Controllers, Models, and Views folder](#Controllers,-Models,-and-Views-folder)
    * [HomeController.cs](#HomeController.cs)
    * [How to display the footer and the menu on the index page?](#How-to-display-the-footer-and-the-menu-on-the-index-page?)
* [MVC Architecture](#MVC-Architecture)
* [Routing](#Routing)
* [Section](#Section)
* [HomeController.cs](#HomeController.cs)
* [Database](#Database)
    * [Create a table](#Create-a-table)
    * [Use statements](#Use-statements)
    * [How to display the entries table on a page](#How-to-display-the-entries-table-on-a-page)
    * [Add category with button](#Add-category-with-button)
    * [Add Validation](#Add-Validation)
    * [Edit Entry](#Edit-Entry)
    * [Delete Entry](#Delete-Entry)
    * [Display Notification on update/delete/create event](#Display-Notification-on-update/delete/create-event)
* [Design](#Design)
* [Razor Pages](#Razor-Pages)
    * [Pages folder](#Pages-folder)
    * [Configure Entity Framework Core](#Configure-Entity-Framework-Core)
* [N-tier architecture](#N-tier-architecture)
* [Repository Pattern](#Repository-Pattern)
    * [Introduction to Repository Pattern](#Introduction-to-Repository-Pattern)
    * [Benefits of Using the Repository Pattern](#Benefits-of-Using-the-Repository-Pattern)
    * [Implementation in ASP.NET Core MVC (.NET 8)](#Implementation-in-ASP.NET-Core-MVC-(.NET-8))
    * [Best Practices and Considerations](#Best-Practices-and-Considerations)
    * [Conclusion](#Conclusion)
* [Identity](#Identity)
* [Utilities](#Utilities)
* [Exercise](#Exercise)
* [Publish your webApp on Azure](#Publish-your-webApp-on-Azure)
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
* [Visual Studio Code](https://visualstudio.microsoft.com/it/vs/)
  * Install ASP.NET pack 
* [SSMS (for database and sql server and management)](https://learn.microsoft.com/it-it/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16#download-ssms)
  * [How to create localdb](https://www.youtube.com/watch?v=_12OOgKzi7I) 
## Welcome project
### Create a project and execute it
To create .net project firstly you open a window in Visual Studio 2022. In the explorer page click "Create new project". Now the search bar is enabled and in this case, you digit the "MVC" and at this moment appear "asp.net core mvc App..." and you click this entry.
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
  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="8.0.0"/>
    <PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="8.0.0"/>
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="8.0.0"	/>
  </ItemGroup>
</Project>
```
These parameters are found within an ASP.NET Core project file (likely a .csproj file) and define some key settings of the project.
* `<Project Sdk="Microsoft.NET.Sdk.Web">`: This line specifies which SDK is used to build the project. In this case, the Microsoft.NET.Sdk.Web SDK is used, which is specific for ASP.NET Core web application development.
* `<PropertyGroup>`: This is an XML element containing a group of project properties. Within this element, project settings are specified.
* `<TargetFramework>net8.0</TargetFramework>`: This indicates the target framework version for the project. In this specific case, the project targets the .NET 8.0 framework. This framework defines the available APIs and libraries for the application.
* `<Nullable>enable</Nullable>`: This setting enables support for nullable reference types in the project. This allows the compiler to detect and report potential null reference issues during compilation.
* `<ImplicitUsings>enable</ImplicitUsings>`: This enables implicit namespace usage within the project. This means that common namespaces such as System, System.Collections.Generic, etc., do not need to be explicitly specified. The compiler will include them automatically.
* Inside the ItemGroup there are packages that the application uses. 
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

When we create an ASP.NET Core Web Application with an Empty or Razor Pages or MVC or Web API Project Template, Visual Studio automatically creates the appsettings.json file for us, as shown in the image below.

The appsettings.json file is the application configuration file used to store configuration settings such as database connection strings, any application scope global variables, etc. If you open the ASP.NET Core appsettings.json file, you see the following code created by Visual Studio by default.

Note: The appsettings.json file typically resides in the root directory of your ASP.NET Core project. You can add multiple appsettings.json files with different names, such as appsettings.development.json, appsettings.production.json, etc., to manage configuration for different environments (e.g., development, production, staging).

Now, I will add a key named MyCustomKey within this file. To do so, please modify the appsettings.json file as shown below. You must store the value as a key-value pair as a JSON file.

Here’s what each section typically means:

* Logging: Defines the logging level for different components of the application.
* AllowedHosts: Specifies the hosts that the application will listen to.
* MyCustomSettings: A custom section that you define for your own application settings.

Here is an example: 
```

{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "MyCustomKey": "MyCustomKey Value coming from appsettings.json"
}
```

Configuration Sections: The file is typically divided into sections that represent different aspects of the application settings. For example, you might have sections like ConnectionStrings, Logging, or custom sections for your application-specific settings.

Security Consideration: It’s important not to store sensitive information, like passwords or secret keys, directly in appsettings.json. Instead, use secure storage like environment variables, Azure Key Vault, or other secure configuration providers.

appsettings.Development.json can be used when the `ASPNETCORE_ENVIROMENT` value is "Development". For this reason, you can create the appsettings.Production.json and use it if the `ASPNETCORE_ENVIROMENT` value is "Production".

### program.cs

Every ASP.NET Core web applications starts like a console application then turn into web application. When you press F5 and run the application, it starts the executing code in the Program.cs file.




Program.cs contains this code:

```
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllersWithViews();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
```
There are two sections: 
* add some services to our container
* configuration of the http request pipeline

* The first line creates an object of WebApplicationBuilder with preconfigured defaults using the CreateBuilder() method. The CreateBuilder() method setup the internal web server which is Kestrel. It also specifies the content root and reads the application settings file appsettings.json. Using this builder object, you can configure various things for your web application, such as dependency injection, middleware, and hosting environment. You can pass additional configurations at runtime based on the runtime parameters.
* The builder object has the Services() method which can be used to add services to the dependency injection container.
* The AddControllersWithViews() is an extension method that registers types needed for MVC application (model, view, controller) to the dependency injection. It includes all the necessary services and configurations for MVC So that your application can use MVC architecture.
* The builder.Build() method returns the object of WebApplication using which you can configure the request pipeline using middleware and hosting environment that manages the execution of your web application.
* Now, using this WebApplication object app, you can configure an application based on the environment it runs on e.g. development, staging or production. The following adds the middleware that will catch the exceptions, logs them, and reset and execute the request path to '"/home/error" if the application runs on the development environment.
* Note that the method starts with "Use" word means it configures the middleware. The following configures the static files, routing, and authorization middleware respectively.
* The `UseHttpsRedirection()` method configures middleware to redirect HTTP requests to HTTPS 
* The `UseStaticFiles()` method configures the middleware that returns the static files from the wwwroot folder only.
* The `UseRouting()` method refers to the concept of route. A route is a URL pattern that has been mapped to a handler. The handler is typically a Razor page, an action method in an MVC controller, or a middleware. ASP.NET Core routing allows you to control the URLs used by the app.
* The `UseAuthorization()` middleware is responsible for handling authorization logic for incoming requests in the ASP.NET Core application, determining whether users have the necessary permissions to access protected resources.
* The MapControllerRoute() defines the default route pattern that specifies which controller, action, and optional route parameters should be used to handle incoming requests. The ? indicates that a parameter can be defined.
* Finally, `app.Run()` method runs the application and starts listening to the incoming request. It turns a console application into an MVC application based on the provided configuration.

Here there are additional information: https://learn.microsoft.com/it-it/aspnet/core/fundamentals/?view=aspnetcore-8.0&tabs=windows#programcs[https://learn.microsoft.com/it-it/aspnet/core/fundamentals/?view=aspnetcore-8.0&tabs=windows#programcs]

### Controllers, Models, and Views folder
They define the MVC keyword. You remember that MVC stands for model views and controller, but how do all three of them come together?

### HomeController.cs
The code of HomeController.cs is:
```
using System.Diagnostics;
using Microsoft.AspNetCore.Mvc;
using BulkyWeb.Models;

namespace BulkyWeb.Controllers;

public class HomeController : Controller
{
    private readonly ILogger<HomeController> _logger;

    //constructor for class
    public HomeController(ILogger<HomeController> logger)
    {
        _logger = logger;
    }

    //from here there are action methods
    public IActionResult Index()
    {
        return View();
    }

    public IActionResult Privacy()
    {
        return View();
    }

    [ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, NoStore = true)]
    public IActionResult Error()
    {
        return View(new ErrorViewModel { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
    }
}
```
In this specific case, there are three action methods. For example, when I digit https://localhost:55555/index I will call the Index() method action, which returns the View(). What does it mean? This method returns some views inside the 'views' folder, but how does the 'views' folder choose the HTML file if in the method there aren't parameters? In this case, the default parameter is the name of the action method that calls the View() function. In addition, the file is selected from the folder with the name in [name]Controller.cs.

The return type "IActionResult" defines a contract that represents the result of an action method. In short, IActionResult is a common return type used in controller action methods in ASP.NET Core MVC to return the result of an operation to the client. Being an interface, it allows great flexibility in the type of result that can be returned.

![HomeControllerCsWorkflow](https://github.com/SimoneMoreWare/learn-asp.net-core-MVC-.net-8-/blob/main/img/HomeControllerCsWorkflow.png)

### How to display the footer and the menu on the index page?
The solution is found in the "views" folder, in particular in the "shared" folder, the "_ViewImports.cshtml" file, and the "_viewStart.cshtml" file. Firstly, there are the master page and child. The master page is identified by underscore ( _ ). The child is identified without underscore. On the master page, is the RenderBody(), which returns the controller's HTML code. In addition, in "_Layout.cshtml" there are declarations of scripts and CSS styles, used globally in the app.  
The "_ValidationScriptsPartial.cshtml" is specifically designed to include the scripts required for model validation in forms. Model validation is a central feature in many web applications, and including the related scripts in _ValidationScriptsPartial.cshtml makes it easier to maintain and manage this part of the code separately from other functionalities of the application. Including model validation scripts here ensures that they are available on all pages where they are needed. In contrast, in the "_Layout.cshtml" there are basic Javascript scripts. The underscore (_) in "_ValidationScriptsPartial.cshtml" doesn't have a specific meaning in terms of ASP.NET syntax or naming conventions. However, commonly, the underscore is used as a prefix in file names to indicate that the file is a "partial view". A partial view in ASP.NET MVC is a type of view that can be embedded within other views or layouts. It's typically used to reuse common user interface components or to organize code in a modular and maintainable way. So, "_ValidationScriptsPartial.cshtml" could be understood as a partial view that contains the scripts necessary for model validation in forms.

The `_ViewStart.cshtml` file in ASP.NET Core MVC is used to define basic settings for views within a specific directory (and optionally its subdirectories). Its content is usually very brief and simple.

`_ViewImports.cshtml` is a feature in ASP.NET Core MVC that enables you to add common namespaces, directives, and other elements to multiple views within your application without having to add these namespaces, directives, and other elements to every individual view file. It essentially serves as a way to include common code that should be available to all views in the same directory or in directories. The _ViewImports.cshtml file works similarly to how web.config or app.config files work for configuration settings, specifically Razor views. The directives that can typically be placed in _ViewImports.cshtml are as follows:

* @using: The @using directive is used to include the common namespaces globally so that you don’t have to include the namespaces in each and every view page.
* @inject: The @inject directives specify a way to inject services from the dependency injection container directly into the view. So, it supports Dependency Injection in a Razor view.
* @model: The @model directive is used to specify the Model for your view. 
* @addTagHelper: Allows you to add Tag Helpers to all views. Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.
* @removeTagHelper: Removes a previously added Tag Helper from the available set.
* @tagHelperPrefix: Sets a prefix that must be used for Tag Helper attributes. This can help to clarify which attributes are intended for server-side processing.

## MVC Architecture
The MVC architecture is divided into three parts:
* Model
  * Represents the shape of the data 
* View
  * Represents the user interface
  * This is control the HTML element of your web project
* Controller
  * Handles the user request and acts as an interface between Model and View.
  * For example, when the user clicks the button the request will first go to the controller. In this case, the controller will then determine what model it has to fetch it will retrieve all the data that is needed using models. As a result, all data is to be displayed in the view component. This component adds all data to its HTML. Besides, the view controller passes data to the controller. Finally, the controller will send a response back to the user, which is visible on the screen.
  * Is the heart of the application.
  * It has many action methods. These methods define the endpoints in a controller

![imageMVCArchitecture](https://github.com/SimoneMoreWare/learn-asp.net-core-MVC-.net-8-/blob/main/img/MVCarchitecture.png)
![imageMVCArchitecture2](https://github.com/SimoneMoreWare/learn-asp.net-core-MVC-.net-8-/blob/main/img/MVCarchitecture2.png)

## Routing
The URL pattern for routing is considered after the domain name. For example of URL is 'https://localhost:55555/{controller}/{action}/{id}

## Section

Sections in ASP.NET Core MVC are a feature that allows you to define specific areas within a layout file that can be filled with content from pages that use that layout. This is useful when you want to maintain the general structure of the layout but insert dynamic content into various sections.

In the layout file (typically named _Layout.cshtml), you can define sections using the @section tag. For example:
```
<!DOCTYPE html>
<html>
<head>
    <title>@ViewData["Title"] - My ASP.NET Application</title>
</head>
<body>
    <header>
        <h1>Welcome to my website!</h1>
    </header>

    <div>
        @RenderBody()
    </div>

    <footer>
        <p>Copyright © 2024 - My Website</p>
        @RenderSection("Footer", required: false)
    </footer>
</body>
</html>
```

Meanwhile, in the view folder, you create a custom section like this:
```
@section Footer {
    <p>This is the footer content for this page.</p>
}

```

## Database
You follow prerequisite instructions before starting with this. 

Firstly, you should create a Category.cs in the folder "models".
```
using System.ComponentModel.DataAnnotations;

namespace BulkyWeb.Models
{
    public class Category
    {
        //here we will create multiple properties, which are the columns that we want in category table 
        [Key]
        public int Id { get; set; } //primary key of the table 
        [Required]
        public required string Name { get; set; }
        public int DisplayOrder { get; set; }
    }
}
```

At the moment to start the database, you create a connection string in appsettings.json, in particular, you should follow this syntax:
`"ConnectionStrings": { "DefaultConnection": "Server=${nameServer};Database=${nameSolution};Trusted_Connection=True;TrustServerCertificate=True" } `

Now, you will install different NuGet packages:
* Microsoft.EntityFrameworkCore
* Microsoft.EntityFrameworkCore.SqlServer
* Microsoft.EntityFrameworkCore.Tools

At the moment, in the "Project File" there are the new package references.

As a result, you should create a new folder in the project to use the database. You will write this code, in this case the folder calls "ApplicationDbContext":

```
using Microsoft.EntityFrameworkCore;

namespace BulkyWeb.Data
{
    public class ApplicationDbContext : DbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options): base(options)
        {
            
        }
    }
}
```

Entity Framework (EF) is an Object-Relational Mapping (ORM) framework developed by Microsoft to simplify data access and management in a relational database using objects. Essentially, EF allows you to work with database data using object-oriented programming (OOP) instead of writing SQL queries directly.

When using EF with ASP.NET Core MVC to interact with a database, one of the main components you'll use is the DbContext. DbContext is a class provided by Entity Framework that represents the working session with the database. It coordinates read and write operations, manages transactions, and tracks changes to data within the context of the working session.

To use a DbContext with Entity Framework in an ASP.NET Core MVC application, you need to define a class that derives from DbContext and includes properties representing database tables. Additionally, you can define relationships between tables and configure other mapping options between model objects and database tables.

Now, in the "Program.cs" you should add a new service into the container. 
```
using BulkyWeb.Data;
...
builder.Services.AddDbContext<ApplicationDbContext>(options => options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"))); 
var app = builder.Build();
```

At the moment, you open the NuGet package console. You select Tools > NuGet Package Manager > Package Manager Console. Now, the console is open, and you digit "update-database". On the display should be appear this message: 
`No migrations were applied. The database is already up to date. No migrations were applied. The database is already up to date. Done. `
This is a notification generated by Entity Framework Core when using ASP.NET Core MVC with .NET 8. It indicates that no changes have been made to the database because no migrations were applied. The message "No migrations were applied" means that there were no migrations to apply, and "The database is already up to date" indicates that the database is already updated to the latest version of the schema defined in the database context. In short, no migration actions were performed because there were no changes in the database schema.

As a result, there is a new database called "Bulky".

### Create a table
Before we created Category.cs class. This class will be used to create a table with 3 columns (every propriety in a class is a column).

For creating a new category table you digit this line into ApplicationDbContext.cs:
`public DbSet<Category> Categories { get; set; }`

How to add a new table to the SQL server? Open the NuGet package console and digit "Add migration". As a result, a new "migration" folder is created in the project. If you digit "update-database" in the NuGet console and refresh the page server, there will be a new category table and the migration table to update.

Here there is a summary of create a table:
* Create class in the model folder
* In the applicationDbContext create a DbSet
* In the NuGet Package Console "add-migration Add${nameClassFirstPoint}TableToDb"
* Now, digit "update-database" to push migration to the database.

### Use statements 
When the category table is created if you want to use statements such as "Select, From, and Delete" you should use the controller. For this reason, you should create a new empty controller in the "Controller" folder, which you call "${nameTable}Controller.cs". If you create a new controller you will create a new view. In the view folder you create a new folder called "${nameTable}". If you want use a new controller in the page you can edit the "_layout.cshtml" and correctly use the asp-controller and asp-action.

In ASP.NET Core MVC (.NET 8), `asp-controller` and `asp-action` are attributes used to define controllers and corresponding actions in an MVC application. These attributes are commonly used in Razor views to generate URLs dynamically.

- `asp-controller`: This attribute is used to specify the name of the controller associated with an action. For example, if you want to link an action to a controller named `HomeController`, you would use `asp-controller="Home"` in the HTML element.

- `asp-action`: This attribute is used to specify the name of the action within the controller. For example, if you want to link to an action called `Index` within the `HomeController`, you would use `asp-action="Index"` in the HTML element.

For instance, if you want to create a link to a specific action in a Razor view, you would use these attributes to define the desired controller and action. Here's an example of how a link might appear in a Razor view:

`<a asp-controller="Home" asp-action="Index">Home</a>`

This will generate a link that points to the Index action within the HomeController. At runtime, ASP.NET Core MVC will translate these attributes into a valid URL for the corresponding action and controller.

### How to display the entries table on a page

The following code snippet in "ApplicationDBContext.cs" is part of the data model configuration when using Entity Framework Core in an ASP.NET Core MVC application:
```
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Category>().HasData(
            new Category { CategoryId=1, Name="Action", DisplayOrder=1},
            new Category { CategoryId=2, Name="SciFi", DisplayOrder=2},
            new Category { CategoryId=3, Name="History", DisplayOrder=3}
        );
}
```
The HasData method is used to specify initial data to be seeded into the database for the Category entity. It allows you to populate the database with samples or initial data. In this case, it's populating the Category table with three categories: "Action", "SciFi", and "History", each with a unique CategoryId and specified display order.

As a result, open NuGet terminal and you digit "add-migration Seed${nameTable}Table". Afterward, you should digit "update-database" to update the database.

For showing the entries table you edit the controller and view the corresponding Category. 
Firstly, edit the CategoryContrller with this code:
```
using BulkyWeb.Data;
using BulkyWeb.Models;
using Microsoft.AspNetCore.Mvc;

namespace BulkyWeb.Controllers
{
    public class CategoryController : Controller
    {
        private readonly ApplicationDbContext _db;
        public CategoryController(ApplicationDbContext db) 
        { 
            _db = db;
        }
        public IActionResult Index()
        {
            List<Category> objCategoryList = _db.Categories.ToList();
            return View(objCategoryList);
        }
    }
}
```

This code snippet represents an ASP.NET Core MVC controller to handle operations related to categories (`Category`) within a web application. Let's examine step by step what it does:

1. **Namespace and using statements:**
   - The controller is defined within the `BulkyWeb.Controllers` namespace.
   - Some using statements are used to include necessary namespaces, such as `BulkyWeb.Data`, `BulkyWeb.Models`, and `Microsoft.AspNetCore.Mvc`.

2. **Controller definition:**
   - `CategoryController` is a class that inherits from the `Controller` class. This indicates it is a controller for operations related to categories.

3. **Constructor:**
   - A constructor is defined for the `CategoryController` that takes an object of type `ApplicationDbContext` as a parameter. This parameter is used for database access.

4. **`Index()` method:**
   - This method handles the HTTP GET request for the `/Category/Index` endpoint.
   - Within the method, a list of `Category` objects is retrieved from the database using the `ApplicationDbContext` object saved in the `_db` variable.
   - The list of categories is then passed to the view associated with the method and returned as the result of the request.

When the objCategoryList (which is ad list of Category objects retrieved from the database) is passed as a parameter to the View() method, it's essentially being passed to the corresponding Razor view file (*.cshtml in this case). This allows the view to access and render the data within that list.

In the Razor view file (*.cshtml), you can use Razor syntax to iterate through objCategoryList and display the categories in HTML.

Here the index.cshtml file:
```
@model List<Category>

<h1>Category List</h1>
<table class="table table-bordered table-striped">
	<thead>
		<tr>
			<th>
				Category Name
			</th>
			<th>
				Display Order
			</th>	
		</tr>
	</thead>
	<tbody>
		@foreach(var obj in Model)
		{
			<tr>
				<td>@obj.Name</td>
				<td>@obj.DisplayOrder</td>
			</tr>
		}
	</tbody>
</table>
```

@model List<Category>: This line specifies the type of model that this view expects. In this case, it's a List of Category objects.

foreach(var obj in Model): This foreach loop iterates through each Category object in the Model, which is the list of categories passed from the controller. For each iteration, the current Category object is stored in the variable obj.

@obj.Name and @obj.DisplayOrder: Within the loop, @obj.Name and @obj.DisplayOrder are Razor syntax used to access properties of the current Category object (obj). This syntax is used to directly output the value of the corresponding properties (Name and DisplayOrder) of each Category object in the table row (<tr>).

Razor syntax (@) allows you to seamlessly mix C# code with HTML markup in Razor views. When you use @obj.Name, it's essentially calling the getter method for the Name property of the Category object (obj). This is a convenient way to access and display properties of objects passed to the view from the controller.

### Add category with button

You should be follow these step:
* Create an action method that will be invoked in the CategoryController.cs
* Call the view (or RedirectToAction?) though action

Here there is the create category page:
```
@model Category

<form method="post">
    <div class="border p-3 mt-4">
        <div class="row pb-2">
            <h2 class="text-primary">Create Category</h2>
            <hr />
        </div>
        <div class="mb-3 row p-1">
            <label asp-for="Name" class="p-0"></label>
            <input asp-for="Name" class="form-control" />
        </div>
        <div class="mb-3 row p-1">
            <label asp-for="DisplayOrder" class="p-0"></label>
            <input asp-for="DisplayOrder" class="form-control" />
        </div>

        <div class="row">
            <div class="col-6 col-md-3">
                <button type="submit" class="btn btn-primary form-control">Create</button>
            </div>
            <div class="col-6 col-md-3">
                <a asp-controller="Category" asp-action="Index" class="btn btn-secondary border  form-control">
                    Back to List
                </a>
            </div>
        </div>


    </div>
</form>
```
Input fields are linked to parameters of the category class. For this scope, you should be used inside the input field "asp-for=${parameter}"

Here's how it works:

1. **Data Binding:** When a form is submitted to the page, the values of the input controls inside the form need to be sent to the server. `asp-for` helps create this association between the field of the model object and the HTML input control. When the page is rendered, the value of the model object is automatically used to populate the field of the input element.

2. **Maintaining Data Binding:** During the postback of the page, such as when a form is submitted, ASP.NET Core uses the values sent in the body of the HTTP request to automatically update the corresponding data model. By using `asp-for`, input controls can be directly associated with members of the data model, simplifying the process of retrieving values during postback.

However, you create a new method action in the CategoryController.

[HttpPost]
public IActionResult Create(Category obj)
{
	_db.Categories.Add(obj);
	_db.SaveChanges();
	return RedirectToAction("Index");
}

Attribute Declaration:

[HttpPost]: This attribute specifies that the action method Create should only respond to HTTP POST requests. In ASP.NET Core MVC, actions can be decorated with attributes to define the type of HTTP request they handle.
Action Method Declaration:

public IActionResult Create(Category obj): This declares the action method Create, which takes a parameter obj of type Category. The Category class represents a category object in the application.
Data Processing:

_db.Categories.Add(obj);: This line adds the Category object obj to the database context _db. The _db represents an instance of the ApplicationDbContext class, which is used for interacting with the application's database.
Database Save:

_db.SaveChanges();: This line saves the changes made to the database context. In this case, it commits the addition of the new category object to the database. This method call persists changes to the underlying database.
Redirection:

return RedirectToAction("Index");: After successfully adding the category to the database, the action method redirects the user to the Index action of the same controller. RedirectToAction is a method provided by ASP.NET Core MVC for redirecting to another action within the same controller or a different controller.

### Add Validation

Add validation in asp.net core mvc .net 8 is a piece of cake. In the class Category.cs write this snippet:

```
using System.ComponentModel;
using System.ComponentModel.DataAnnotations;

namespace BulkyWeb.Models
{
    public class Category
    {
        //here we will create multiple properties, which are the columns that we want in category table 
        [Key]
        public int CategoryId { get; set; } //primary key of the table 
        [Required]
        [MaxLength(30)] 
        [DisplayName("Category Name")]
        public required string Name { get; set; }
        [DisplayName("Display Order")]
        [Range(1,100,ErrorMessage = "You're a dumb")]
        public int DisplayOrder { get; set; }
    }
}
```

However, implement custom validation on the create page you must be edit the action method in the controller.
```
[HttpPost]
public IActionResult Create(Category obj)
{
    if (ModelState.IsValid) { 
	    _db.Categories.Add(obj);
	    _db.SaveChanges();
            return RedirectToAction("Index");
	}
    return View();
}
```
The (ModelState.IsValid) condition is commonly used in ASP.NET Core MVC controller actions to check whether the model passed to the action is valid based on the validation rules defined in the model class. Let's break down what it does:

* ModelState: ModelState is a property of the controller class in ASP.NET Core MVC that represents the state of model binding and validation. It contains information about the state of each property of the model being bound.
* IsValid: The IsValid property is a boolean property of the ModelState object. It indicates whether the model state is valid or not based on the validation rules defined for the properties of the model.
* Usage: (ModelState.IsValid) is typically used within controller actions to perform conditional logic based on the validity of the model. If the model state is valid, meaning that all the validation rules defined for the properties of the model have been satisfied, then the condition (ModelState.IsValid) evaluates to true. Otherwise, it evaluates to false.

How to implement error in the create page? You add 
`<span asp-validation-for="${nameParameter" class="text-danger"></span>`

if you want to add a specific message error when the specific event happened you should use it to
```
if (obj.Name == obj.DisplayOrder.ToString())
{
    ModelState.AddModelError("name", "The DisplayOrder cannot exactly match the Name.");
}
```
`AddModelError` is a method used in the controller of an ASP.NET Core MVC application to add a model error to the `ModelState`. This method is useful when you want to customize validation errors and add a specific error message for a particular model property.

Here's what `AddModelError` is used for and how it's used:

1. **Customizing validation errors**: When validating a model in the controller, validation errors may occur, such as if a required field has not been filled in correctly. In these cases, you can use `AddModelError` to add a custom error message for a specific model property.

2. **Custom error messages**: `AddModelError` allows you to specify a custom error message to be displayed for a specific model property. This can be useful for providing users with more detailed information about what went wrong during model validation.


The `<div asp-validation-summary="All"></div>` tag in an ASP.NET Core MVC Razor view is used to display a summary of model validation errors.

The validation summary will typically display a list of error messages for each invalid field in the model. The exact format and style of the summary may depend on the CSS styles applied to it.

The "All" option specified in asp-validation-summary="All" ensures that all validation errors are included in the summary, regardless of which fields they are associated with.

There are only three valid values for the asp-validation-summary attribute in ASP.NET Core MVC Razor views:
* "All": Displays a summary of all validation errors, including errors associated with individual properties as well as errors associated with the model as a whole.
* "ModelOnly": Displays a summary of errors associated with the model as a whole, excluding errors associated with individual properties.
* "None": Specifies that no validation summary should be displayed. It essentially disables the validation summary feature.

### Edit Entry

You should create a new method action called "Edit". However, you should create a view edit page.

There are two methods of action.
```
public IActionResult Edit(int? id)
{
    if(id==null || id == 0)
    {
        return NotFound();
    }
    Category? categoryFromDb = _db.Categories.Find(id);
    //Category? categoryFromDb1 = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //Category? categoryFromDb2 = _db.Categories.Where(u=>u.Id==id).FirstOrDefault();

    if (categoryFromDb == null)
    {
        return NotFound();
    }
    return View(categoryFromDb);
}
[HttpPost]
public IActionResult Edit(Category obj)
{
    if (ModelState.IsValid)
    {
        _db.Categories.Update(obj);
        _db.SaveChanges();
        return RedirectToAction("Index");
    }
    return View();

}
```
`public IActionResult Edit(int? id)`
This method handles the GET request for editing a category in an ASP.NET Core MVC application. Here's what the main parts of the method do:
- Checks if the `id` is valid. If the `id` is null or zero, it returns a "NotFound" result.
- Retrieves the category from the database using the `Find()` method. It searches for the entity with the specified primary key.
- If the category is not found in the database, it returns a "NotFound" result.
- If the category is found, it returns the `Edit` view with the category as the model.
- In index.cshtml used asp-route-id to pass the parameter id.
    - asp-route-id="@obj.Id"
    - In an ASP.NET Core MVC application, `asp-route-id="@obj.Id"` is used to generate a URL with a route parameter called "id", whose value will be taken from the "Id" property of the `obj` object.
    - When a link is generated using `asp-route`, it creates a URL that includes the specified route parameters. In your case, `asp-route-id="@obj.Id"` means that a URL will be generated with a route parameter called "id" whose value will be the ID of the `obj` object.
    - For example, if `obj.Id` is 1, the generated URL will be something like this:
        - /ControllerName/ActionName?id=1
        - This URL will be used to call a specific action in the controller with the ID as a parameter. This is useful when you want to pass data between different actions or pages within the application.

`[HttpPost] public IActionResult Edit(Category obj)`
This method handles the POST request when the category edit form is submitted. Here's what the main parts of the method do:
- Checks if the model is valid, i.e., if the submitted data satisfies the validation rules defined in the `Category` model.
- If the model is valid, updates the category in the database using the `Update()` method of the database context (`_db`). This method marks the entity as modified and adds it to the set of entities to be updated.
- Calls `SaveChanges()` to actually perform the update in the database.
- If the update is successful, redirects the user to the "Index" action of the controller, typically representing the list of categories.
- If the model is not valid (e.g., due to validation errors), returns the `Edit` view with the category model to allow the user to correct the data.

Functions Used:
- `Find(int? id)`: Searches for an entity in the current entity set using the specified primary key. Returns the found entity or null if not found.
- `FirstOrDefault()`: Returns the first element of a sequence or the default value of the type if the sequence is empty.
- `Where()`: Filters a sequence of values based on a specified predicate. Returns the elements that satisfy the predicate as a sequence.
- `Update()`: Marks an entity as modified and adds it to the set of entities to be updated in the database context.
- `NotFound()`: Returns an HTTP "404 Not Found" result. This method is often used to indicate that a requested resource was not found on the server.

### Delete Entry

You should create a new method action called "Delete". However, you should create a view delete page.

There are two methods of action:
```
public IActionResult Delete(int? id)
{
    if (id == null || id == 0)
    {
        return NotFound();
    }
    Category? categoryFromDb = _db.Categories.Find(id);
    //Category? categoryFromDb1 = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //Category? categoryFromDb2 = _db.Categories.Where(u=>u.Id==id).FirstOrDefault();

    if (categoryFromDb == null)
    {
        return NotFound();
    }
    return View(categoryFromDb);
}
[HttpPost, ActionName("Delete")]
public IActionResult DeletePOST(int? id)
{

    Category obj = _db.Categories.Find(id);

    if (obj == null)
    {
        return NotFound();
    }

    _db.Categories.Remove(obj);
    _db.SaveChanges();
    return RedirectToAction("Index");

}
```
`public IActionResult Delete(int? id)`
1. The method `Delete` is an HTTP GET action method, which handles requests to display a form to delete a category.
2. It takes an optional parameter `id`, representing the ID of the category to be deleted.
3. Checks if the `id` is null or zero. If so, it returns a "NotFound" result, indicating that the category was not found.
4. Retrieves the category with the specified `id` from the database using the `Find` method.
5. If the category is not found (`categoryFromDb` is null), it returns a "NotFound" result.
6. Otherwise, it returns a view to display the details of the category to be deleted.
7. In index.cshtml used asp-route-id to pass the parameter id.
    - asp-route-id="@obj.Id"
    - In an ASP.NET Core MVC application, `asp-route-id="@obj.Id"` is used to generate a URL with a route parameter called "id", whose value will be taken from the "Id" property of the `obj` object.
    - When a link is generated using `asp-route`, it creates a URL that includes the specified route parameters. In your case, `asp-route-id="@obj.Id"` means that a URL will be generated with a route parameter called "id" whose value will be the ID of the `obj` object.
    - For example, if `obj.Id` is 1, the generated URL will be something like this:
        - /ControllerName/ActionName?id=1
        - This URL will be used to call a specific action in the controller with the ID as a parameter. This is useful when you want to pass data between different actions or pages within the application.

`[HttpPost, ActionName("Delete")] public IActionResult DeletePOST(int? id)`
1. The method `DeletePOST` is an HTTP POST action method, which handles form submissions to delete a category.
2. It takes an optional parameter `id`, representing the ID of the category to be deleted.
3. Retrieves the category with the specified `id` from the database using the `Find` method and assigns it to the `obj` variable.
4. Checks if the `obj` is null. If so, it returns a "NotFound" result, indicating that the category was not found.
5. Removes the `obj` from the database using the `Remove` method of the database context (`_db`).
6. Calls `SaveChanges` to persist the changes to the database.
7. Redirects the user to the "Index" action of the controller, typically representing the list of categories.

Functions Used:
- `Find(int? id)`: Searches for an entity in the current entity set using the specified primary key. Returns the found entity or null if not found.
- `Remove(obj)`: Marks the specified entity for deletion. The entity will be deleted from the database when `SaveChanges` is called.
- `SaveChanges()`: Persists all changes made to entities in the database context to the underlying database.
- `NotFound()`: Returns an HTTP "404 Not Found" result. This method is often used to indicate that a requested resource was not found on the server.

In the delete view page used `<input asp-for="Id" hidden />` that generates a hidden input field for the "Id" property of the model associated with the view. This can be useful for passing values between the client and server without displaying them to the user. The value of the "Id" property will be sent along with other form data when the form is submitted, but it won't be visible to the user in the browser.
This can be particularly helpful in scenarios like form submissions where you need to send the ID of an entity to the server without exposing it to the user.

### Display Notification on update/delete/create event

Create custom css toastr: https://codeseven.github.io/toastr/demo.html

For this scope, there is TempData

In ASP.NET Core MVC, TempData is a feature that allows us to store temporary data that will be available for the next request. It’s a mechanism to pass data between different actions or controllers during the lifetime of a user’s session. TempData is typically used when you want to show a message or provide some information to the user after a redirect.

TempData is implemented using the session state. It stores data in the session between requests, but unlike regular session data, TempData is meant to be short-lived and is removed automatically once read or after the subsequent request is processed.

The TempData in ASP.NET Core MVC Application is one of the mechanisms to pass a small amount of temporary data from a controller action method to a view and from a controller action method to another action method within the same controller or to a different controller. TempData value will become null once the subsequent request is completed by default. But if you want, then you can also change this default behavior. If you look at the definition Controller class, you will find the following signature of the TempData property.

Once TempData data is read, it's automatically marked for deletion. This means TempData data will be available only for the subsequent request and will be deleted after being read. This behavior is useful for passing temporary information, such as confirmation messages or errors, between actions.

TempData is often used to pass feedback messages, such as success messages or errors, between actions. For example, after completing a save operation, you can store a success message in TempData and then redirect the user to a display page with the success message displayed. Alternatively, in case of errors, you can store an error message in TempData and redirect the user to the previous page with the error message displayed.

In this case, use the partial view, here is the code:
```
@if (TempData["success"] != null)
{
    <script src="~/lib/jquery/dist/jquery.min.js"></script>
    <script src="//cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/js/toastr.min.js"></script>
    <script type="text/javascript">
        toastr.success('@TempData["success"]');
    </script>
}
@if (TempData["error"] != null)
{
    <script src="~/lib/jquery/dist/jquery.min.js"></script>
    <script src="//cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/js/toastr.min.js"></script>
    <script type="text/javascript">
        toastr.success('@TempData["error"]');
    </script>
}
```


## Design
Tool: (https://bootswatch.com/)[https://bootswatch.com/]

With this tool you choose a lot templates for your project. Download the bootstrap.css and put the code in bootstrap lib in the wwwroot folder (wwwroot->lib->bootstrap->bootstrap.css)

Tool: (https://icons.getbootstrap.com/)[https://icons.getbootstrap.com/]

Include the icon fonts stylesheet—in your website <head>  
`<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">`

## Razor Pages

**Overview:**
Razor Pages are a feature of ASP.NET Core that allows for quickly creating web pages without the need for a separate controller. Razor Pages offer a simple and intuitive way to handle HTTP requests and generate HTML responses using a file-based model.

**Simplicity:**
Razor Pages are designed to simplify web page development, especially for CRUD (Create, Read, Update, Delete) scenarios. Each Razor Page consists of a .cshtml file that combines HTML markup and C# code.

**Routing based on Page Name:**
Razor Pages use routing based on the page name, which means the URL structure corresponds to the directory and file structure in the Razor Pages project. For example, a Razor Page named Index.cshtml located in the Pages/ directory will be accessible via the /Index URL.

Difference between Razor pages and MVC
**Code Structure and Organization:**

Razor Pages: In Razor Pages, the code structure is organized around the pages themselves. Each Razor Page includes both HTML markup and page processing logic within the same .cshtml file. The page handling logic is encapsulated within a PageModel class associated with the page itself.

Model-View-Controller (MVC): In MVC, the code structure is organized around three main components: Model, View, and Controller. The Model contains the business logic and application data, the View handles the presentation of the user interface, and the Controller manages user requests and coordinates actions between the Model and View.

**Routing:**

Razor Pages: Razor Pages use routing based on the page name. The URL structure corresponds to the directory and file structure in the Razor Pages project.

Model-View-Controller (MVC): MVC uses routing based on the [Route] attribute on controller methods. URL paths are mapped to controller methods using ASP.NET Core routing conventions.

**Complexity:**

Razor Pages: Razor Pages are designed to simplify web page development, especially for CRUD (Create, Read, Update, Delete) scenarios. They are ideal for simpler applications or single pages that don't require a full MVC pattern.

Model-View-Controller (MVC): MVC is more flexible and scalable compared to Razor Pages. It's suitable for more complex applications that require greater separation of concerns between Model, View, and Controller.

**Flexibility and Customization:**

Razor Pages: Razor Pages are less flexible compared to MVC but are easier to learn and use, especially for beginner developers or simpler projects.

Model-View-Controller (MVC): MVC offers greater flexibility and customization. You can use filters, middleware, and other advanced ASP.NET Core features to implement more complex requirements.

### Pages folder
Contains Razor pages and supporting files. Each Razor page is a pair of files:

A .cshtml file that has HTML markup with C# code using Razor syntax.
A .cshtml.cs file that has C# code that handles page events.
Supporting files have names that begin with an underscore. For example, the _Layout.cshtml file configures UI elements common to all pages. _Layout.cshtml sets up the navigation menu at the top of the page and the copyright notice at the bottom of the page. For more information, see Layout in ASP.NET Core.

### Configure Entity Framework Core

The first step is to create a new folder called "Models". In the "Models" folder create a class Category.cs.

However, you create a new connection string in the appsetting.json (read before paragraph about this).

To add the nuget packages you click on the solution bar and with the right mouse button you can install new packages through nuget manager. You should remember to edit the project file. 

To configure the entity framework you should create a new folder called "Data". In this folder, you create the class of ApplicationDbContext.cs.

In addition, you add a configuration string to connect the database in the program.cs.

Now, there are migration and creation tables.

THE SNIPPET CODE IS THE SAME PREVIOUS CHAPTER (MVC) IN THIS PASSAGE.

Now, create a new folder called "Categories" in the "Pages". Now, create a index.cshtml in the "categories" folder.

Here is the code:
Index.cshtml.cs
```
using BulkyWebRazor_Temp.Data;
using BulkyWebRazor_Temp.Models;
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;

namespace BulkyWebRazor_Temp.Pages.Categories
{
    public class IndexModel : PageModel
    {
        private readonly ApplicationDbContext _db;
        public List<Category> CategoryList { get; set; }
        public IndexModel(ApplicationDbContext
            db)
        {
            _db = db;
        }
        public void OnGet()
        {
            CategoryList = _db.Categories.ToList();
        }
    }
}
```
Namespaces and Dependencies:

It includes necessary namespaces such as Microsoft.AspNetCore.Mvc, Microsoft.AspNetCore.Mvc.RazorPages, BulkyWebRazor_Temp.Data, and BulkyWebRazor_Temp.Models.
It declares a dependency on ApplicationDbContext for database operations.
PageModel Class:

It defines a class named IndexModel that inherits from PageModel. In Razor Pages, each page has a corresponding PageModel class responsible for handling the page's logic.
It declares a private readonly field _db of type ApplicationDbContext. This field will be used to access the database.
It declares a public property CategoryList of type List<Category>. This property will hold the list of categories retrieved from the database.
Constructor:

It defines a constructor for IndexModel that accepts an instance of ApplicationDbContext (db) as a parameter.
Inside the constructor, it assigns the provided db parameter to the private _db field, allowing the PageModel to interact with the database.
OnGet Method:

It defines an OnGet method, which is invoked when the page is requested using the HTTP GET method.
Inside the OnGet method, it retrieves a list of categories from the database using _db.Categories.ToList().
It assigns the retrieved list of categories to the CategoryList property, making it available for use in the associated Razor view (Index.cshtml).

Invocation of the OnGet method:
The OnGet method is invoked when the page is requested using the HTTP GET method. When a user navigates to the corresponding page (Index.cshtml in your case), the ASP.NET Core framework automatically executes the OnGet method of the IndexModel class. Within the OnGet method, operations are performed to prepare the data to be displayed on the page. For example, in your code, the OnGet method retrieves a list of categories from the database and assigns it to the CategoryList property.

Prefix "On" in the action methods:
In Razor Pages, the "On" prefix in action method names is a convention used to indicate that the method is called in response to a specific action. For example:

OnGet: This method is called when the page is requested using the HTTP GET method.
OnPost: This method is called when the page receives a form submit using the HTTP POST method.
Other prefixes such as OnPut, OnDelete, etc., are used to handle other types of HTTP requests.
These methods are called "action methods" because they represent the actions that the PageModel can perform in response to HTTP requests. The prefix "On" is used to distinguish these methods as specific event handlers in Razor Pages.

index.cshtml
```

@page
@model BulkyWebRazor_Temp.Pages.Categories.IndexModel

<div class="container">
    <div class="row pt-4 pb-3">
        <div class="col-6">
            <h2 class="text-primary">
                Category List
            </h2>
        </div>
        <div class="col-6 text-end">
            <a asp-page="Categories/Create" class="btn btn-primary">
                <i class="bi bi-plus-circle"></i>  Create New Category
            </a>
        </div>
    </div>

    <table class="table table-bordered table-striped">
        <thead>
            <tr>
                <th>
                    Category Name
                </th>
                <th>
                    Display Order
                </th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            @foreach (var obj in Model.CategoryList.OrderBy(u => u.DisplayOrder))
            {
                <tr>
                    <td>@obj.Name</td>
                    <td>
                        @obj.DisplayOrder
                    </td>
                    <td>
                        <div class="w-75 btn-group" role="group">
                            <a asp-page="Category/edit" asp-route-id="@obj.Id" class="btn btn-primary mx-2">
                                <i class="bi bi-pencil-square"></i> Edit
                            </a>
                            <a asp-page="Category/delete" asp-route-id="@obj.Id" class="btn btn-danger mx-2">
                                <i class="bi bi-trash-fill"></i> Delete
                            </a>
                        </div>
                    </td>
                </tr>
            }
        </tbody>
    </table>

</div>
```
The asp-page attribute in ASP.NET Core Razor Pages is used to generate URLs for navigation within Razor Pages. Here's how it works:

`<a asp-page="PageName">Link Text</a>`

asp-page: This attribute specifies the Razor Page to navigate to. You provide the name of the Razor Page without the file extension (e.g., "PageName" instead of "PageName.cshtml").

Link Text: This is the text or HTML content displayed for the link.

When the Razor Page containing this link is rendered, ASP.NET Core will automatically generate the appropriate URL based on the provided Razor Page name. If the Razor Page is located within a folder, you can include the folder path in the asp-page attribute value (e.g., "FolderName/PageName").

Additionally, you can include route parameters in the URL by specifying them using the asp-route-* attributes. For example:
`<a asp-page="PageName" asp-route-id="123">Link Text</a>`
In this case, "id" is a route parameter, and its value is set to "123". When the link is rendered, ASP.NET Core will generate a URL with the route parameter included, like /PageName?id=123.

Now, you create Create.cshtml page in the same folder.
The create.cshtml.cs code is:
```
using BulkyWebRazor_Temp.Data;
using BulkyWebRazor_Temp.Models;
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;

namespace BulkyWebRazor_Temp.Pages.Categories
{
    [BindProperties]
    public class CreateModel : PageModel
    {
        private readonly ApplicationDbContext _db;
        public Category Category { get; set; }
        public CreateModel(ApplicationDbContext
            db)
        {
            _db = db;
        }
        public void OnGet()
        {
        }

        public IActionResult OnPost()
        {
            _db.Categories.Add(Category);
            _db.SaveChanges();
            return RedirectToPage("Index"); //same folder that it works
        }
    }
}
```

1. **Namespace and Dependencies**:
   - Import necessary namespaces such as `BulkyWebRazor_Temp.Data`, `BulkyWebRazor_Temp.Models`, `Microsoft.AspNetCore.Mvc`, and `Microsoft.AspNetCore.Mvc.RazorPages`.

2. **PageModel Class Declaration**:
   - Declare a class named `CreateModel` that inherits from `PageModel`. This class represents the PageModel for the Create page.

3. **BindProperties Attribute**:
   - Apply the `[BindProperties]` attribute to the `CreateModel` class. This attribute automatically binds properties of the class to the values submitted in HTTP requests.

4. **Private Field and Constructor**:
   - Declare a private readonly field `_db` of type `ApplicationDbContext`. This field is used to access the database.
   - Define a constructor for the `CreateModel` class that accepts an instance of `ApplicationDbContext` (`db`) as a parameter. Inside the constructor, assign the provided `db` parameter to the private `_db` field.

5. **Public Property**:
   - Declare a public property `Category` of type `Category`. This property represents the category to be created.

6. **OnGet Method**:
   - Define an empty `OnGet` method. This method is invoked when the page is requested using the HTTP GET method. In this case, it does not perform any specific logic.

7. **OnPost Method**:
   - Define an `OnPost` method. This method is invoked when the page receives a form submission using the HTTP POST method.
   - Inside the `OnPost` method, add the `Category` object to the `_db.Categories` DbSet to insert it into the database.
   - Call `_db.SaveChanges()` to persist changes to the database.
   - Return a `RedirectToPage` result, redirecting the user to the "Index" page within the same folder.

8. **Conclusion**:
   - This PageModel class handles the creation of a new category. It receives the category data from a form submission, adds it to the database, and then redirects the user to the "Index" page.
  
the code of create.cshtmt is:
```
@page
@model BulkyWebRazor_Temp.Pages.Categories.CreateModel

<form method="post">

    <div class="border p-3 mt-4">
        <div class="row pb-2">
            <h2 class="text-primary">Create Category</h2>
            <hr/>
        </div>
        @*<div asp-validation-summary="ModelOnly"></div>*@
       <div class="mb-3 row p-1">
            <label asp-for="Category.Name"  class="p-0"></label>
            <input asp-for="Category.Name" class="form-control" />
            <span asp-validation-for="Category.Name" class="text-danger"></span>
        </div>
        <div class="mb-3 row p-1">
            <label asp-for="Category.DisplayOrder" class="p-0"></label>
            <input asp-for="Category.DisplayOrder" class="form-control" />
            <span asp-validation-for="Category.DisplayOrder" class="text-danger"></span>
        </div>

        <div class="row">
            <div class="col-6 col-md-3">
                <button type="submit" class="btn btn-primary form-control" >Create</button>
            </div>
            <div class="col-6 col-md-3">
                <a asp-page="/Categories/index" class="btn btn-secondary border  form-control">
                    Back to List
                </a>
            </div>
        </div>
        
       
    </div>
</form>

@section Scripts{
    @{
    <partial name="_ValidationScriptsPartial"/>
    }
}
```
The approach of editing, and deleting pages is the same. This is an assignment.

## N-tier architecture

N-tier architecture, in ASP.NET Core MVC .NET 8 environment, refers to a mode of software design and organization where the application is divided into several distinct layers or tiers, each with a specific purpose. Each tier performs well-defined functions and collaborates with others to provide functionality to the application as a whole. The main tiers of a typical N-tier architecture include:

1. **Presentation Layer**: This is the topmost layer of the application, responsible for presenting the user interface to the end-user and managing user interactions. In an ASP.NET Core MVC application, this role is often performed by controllers and views.

2. **Business Logic Layer**: This layer contains the business logic of the application. Business rules, data validation, and complex processing are implemented here. This layer is often also called the "service" or "service layer".

3. **Data Access Layer**: This layer manages access to underlying data, such as a database or external services. It handles executing queries, updates, and persistence operations on the data. In ASP.NET Core MVC, this layer might include data models, repositories, and data access services.

4. **Infrastructure Layer**: This layer provides support services and utilities for the application, such as logging, exception handling, authentication, authorization, caching, etc. This layer may also include third-party libraries or external components necessary for the application's operation.

Using an N-tier architecture offers several advantages, including greater modularity, maintainability, scalability, and testability of the software. Additionally, by separating various aspects of the application into distinct layers, it becomes easier for developers to manage complexities and make changes without impacting other components of the system.

Benefits of Using N-Tier Architecture in ASP.NET Core MVC on .NET 8

Utilizing an n-tier architecture in an environment like ASP.NET Core MVC on .NET 8 offers several advantages:

1. **Separation of Concerns**: N-tier architecture allows for clear separation of the various responsibilities within your system. For example, you can separate business logic from presentation logic and data handling, improving code maintainability.

2. **Scalability**: Dividing the system into multiple tiers enables more efficient scaling. You can add resources and scale individual tiers separately based on load demands.

3. **Maintainability**: With well-defined layers, it's easier to maintain and update the system. Each layer can be modified or updated independently of the others, reducing the risk of unintended side effects.

4. **Testability**: N-tier architecture promotes better code testability. It's easier to write unit tests for individual components as different tiers can be tested separately, streamlining the testing process.

5. **Reusability**: Separating different layers encourages code reuse. For instance, business logic can be reused across different contexts without having to rewrite it from scratch.

6. **Security**: Proper implementation of n-tier architecture can contribute to enhancing system security. Specific security measures can be applied to each layer, such as data validation at the presentation layer and protection of sensitive data at the data access layer.

Overall, using n-tier architecture in ASP.NET Core MVC on .NET 8 can lead to a more modular, scalable, testable, and maintainable system, providing a solid foundation for developing robust and high-quality web applications.


Example of project: 
* (https://github.com/aghayeffemin/aspnetcore.ntier)[https://github.com/aghayeffemin/aspnetcore.ntier]
* (https://github.com/nuyonu/N-Tier-Architecture)[https://github.com/nuyonu/N-Tier-Architecture]
* (https://www.youtube.com/watch?v=_-PnZ37kSLA)[https://www.youtube.com/watch?v=_-PnZ37kSLA]

## Repository Pattern

Welcome to this tutorial on the Repository Design Pattern in C# and ASP.NET Core MVC applications. In this video, we will explore how to implement the repository design pattern to improve the structure and maintainability of your code.

The Problem with Traditional Approach

If you have ever created a C# ASP.NET MVC application, you may be familiar with the traditional approach of organizing your code. Typically, you would have a controller for each model in your application, such as a product controller for managing products.
In this traditional approach, all the CRUD (create, read, update, delete) operations for the product model would be placed inside the product controller. This may work fine for small applications, but as the application grows and new functionality is added, it can lead to code duplication and maintenance issues.

The Repository Design Pattern

The repository design pattern provides a solution to the problems mentioned above. It introduces an additional layer between the controller and the data access logic. Instead of directly accessing the database context from the controller, the controller communicates with a product repository, which in turn communicates with the context.
This separation of concerns allows for better code organization, easier maintenance, and the ability to reuse the repository in other controllers if needed. It also reduces the risk of duplicating code when adding new functionality.

Implementing the Repository Pattern

To implement the repository pattern, we need to create an interface and a class for the product repository.
In your project, create a folder called "Repositories" to hold your repository classes. Inside this folder, create an interface called "IProductRepository". This interface will define the contract for the product repository.
The "IProductRepository" interface should include methods for CRUD operations, such as "GetAll", "GetById", "Insert", "Update", and "Delete". These methods will be implemented in the product repository class.
Next, create a class called "ProductRepository" inside the "Repositories" folder. This class should implement the "IProductRepository" interface.
In the "ProductRepository" class, you will need to inject the database context using dependency injection. This can be done by adding a constructor that takes an instance of the context.
Inside the constructor, assign the context to a private readonly field. This field will be used to perform data access operations.
Now, you can move the code from the product controller to the product repository class. For example, the "GetAll" method in the repository class will query the context to retrieve all products, while the "Insert" method will create a new product in the database.
Finally, in the product controller, you can replace the direct access to the context with calls to the product repository methods. For example, to get all products, you can call the "GetAll" method on the product repository instead of querying the context directly.
By implementing the repository pattern, you have decoupled the controller from the data access logic and improved the maintainability of your code.

Sure, let's delve into the repository pattern in ASP.NET Core MVC, particularly focusing on .NET 8. 

### 1. Introduction to Repository Pattern
The Repository Pattern is a design pattern commonly used in software development to separate the logic that retrieves data from a data source (such as a database) from the business logic of an application. This pattern helps in promoting a separation of concerns and makes the application more maintainable and testable.

### 2. Benefits of Using the Repository Pattern
- **Abstraction**: Provides an abstraction layer between the application code and the data access code.
- **Testability**: It allows for easier unit testing by enabling mocking of the repository interfaces.
- **Flexibility**: Allows for easy swapping of data access technologies without affecting the business logic.
- **Encapsulation**: Encapsulates the details of data access logic, making it easier to manage and maintain.

### 3. Implementation in ASP.NET Core MVC (.NET 8)
Here's how you can implement the repository pattern in an ASP.NET Core MVC application using .NET 8:

#### a. Define Repository Interfaces
Create interfaces for your repositories to define the contract for data access operations. For example:
```
public interface IRepository<T>
{
    Task<T> GetByIdAsync(int id);
    Task<IEnumerable<T>> GetAllAsync();
    Task AddAsync(T entity);
    Task UpdateAsync(T entity);
    Task DeleteAsync(int id);
}
```

#### b. Implement Repository Classes
Implement the repository interfaces with concrete classes that interact with the data source (e.g., a database). For instance:
```
public class UserRepository : IRepository<User>
{
    private readonly YourDbContext _dbContext;

    public UserRepository(YourDbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public async Task<User> GetByIdAsync(int id)
    {
        return await _dbContext.Users.FindAsync(id);
    }

    // Implement other repository methods...
}
```

#### c. Dependency Injection
Register your repository classes and interfaces with the ASP.NET Core Dependency Injection container in the `Startup.cs` file:
```
public void ConfigureServices(IServiceCollection services)
{
    services.AddScoped<IRepository<User>, UserRepository>();
    // Add other services...
}
```

#### d. Using Repositories in Controllers
Inject the repository interfaces into your controllers and use them to access data within your MVC actions. For example:
```
public class UserController : Controller
{
    private readonly IRepository<User> _userRepository;

    public UserController(IRepository<User> userRepository)
    {
        _userRepository = userRepository;
    }

    public async Task<IActionResult> Index()
    {
        var users = await _userRepository.GetAllAsync();
        return View(users);
    }

    // Implement other controller actions...
}
```

### 4. Best Practices and Considerations
- **Unit of Work Pattern**: Consider combining the Repository Pattern with the Unit of Work pattern for managing transactions and coordinating multiple repositories.
- **Async/Await**: Prefer asynchronous methods for I/O-bound operations to improve scalability and responsiveness.
- **Error Handling**: Implement robust error handling and logging mechanisms in your repository methods.
- **Caching**: Consider caching frequently accessed data to improve performance, especially in read-heavy applications.

### 5. Conclusion
The Repository Pattern is a powerful tool for abstracting data access logic in ASP.NET Core MVC applications, promoting modularity, testability, and maintainability. By following best practices and design principles, you can leverage the repository pattern to build scalable and robust applications in .NET 8.
More information here: (https://medium.com/net-core/repository-pattern-implementation-in-asp-net-core-21e01c6664d7)[https://medium.com/net-core/repository-pattern-implementation-in-asp-net-core-21e01c6664d7]

Conclusion

The repository design pattern is a powerful technique that can greatly improve the structure and maintainability of your C# and ASP.NET Core MVC applications. By separating the data access logic into a separate layer, you can reduce code duplication, improve code organization, and facilitate code reuse.
By implementing the repository pattern, you can easily add new functionality to your application without having to modify the controller code. This can lead to more maintainable and scalable applications.

## Identity
To complete... (also for home page)

## Utilities
* https://bootswatch.com/
* https://icons.getbootstrap.com/
* To receive a good description of the topic you can use this prompt: "Could I receive a comprehensive treatment on the topic [nameTopic], including all relevant details and information?"
* https://www.learnprompt.org/chat-gpt-prompts-for-learning/
* https://github.com/ktaranov/naming-convention/blob/master/C%23%20Coding%20Standards%20and%20Naming%20Conventions.md

## Exercise
* [Custom Identity in Asp.Net Core MVC | Login and User Registration | .Net 8
](https://www.youtube.com/watch?v=93ssXlCPcuI)
* [ecommerce-books-store](https://github.com/itsyst/ecommerce-books-store)
* [GuitarCenterWeb](https://github.com/KrystianMroczkowski/GuitarCenterWeb)
* [The Bookstore Management Web Application](https://github.com/supun-chamika/BookStore-Management-Web-App-using-ASP.NET-Core-MVC-.NET-8-)

## Publish your webApp on Azure
https://www.youtube.com/watch?v=TcghUb1NPCw
