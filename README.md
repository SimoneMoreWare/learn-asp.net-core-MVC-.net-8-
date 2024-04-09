# learn-asp.net-core-MVC-.net-8
My notes about asp.net core MVC [.net 8]

# Video Course
https://www.youtube.com/watch?v=AopeJjkcRvU&t=909s

# Microsoft Official Guide
* https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0&tabs=visual-studio
* https://learn.microsoft.com/it-it/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0&tabs=visual-studio

# Sites
* https://dotnettutorials.net/lesson/viewimports-in-asp-net-core-mvc/#google_vignette
* https://www.tutorialsteacher.com/core/aspnet-core-program

# Project Resources
* https://github.com/bhrugen/Bulky_MVC/tree/15a896555835fae1482fb1536e549dc132c92249

# Notes
## Topic
* [Fundamentals of ASP.NET Core](#Fundamentals-of-ASP.NET-Core)
* [Prerequisites](#Prerequisites)
* [Tools Needed](#Tools-Needed)
* [Welcome project](#Welcome-project)
* [MVC Architecture](#MVC-Architecture)
* [Routing](#Routing)
* [HomeController.cs](#HomeController.cs)
* [Database](#Database)
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
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="8.0.0"/>
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

## Routing
The URL pattern for routing is considered after the domain name. For example of URL is 'https://localhost:55555/{controller}/{action}/{id}

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

###How to display the entries table on a page

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
