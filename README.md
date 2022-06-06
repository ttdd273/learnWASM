# What is Blazor?

Blazor apps are composed of reusable web UI components built using C#, HTML, and CSS. With Blazor, developers can build client and server code with C#. They can also share code and libraries with the front-end client code and back-end logic. Using C# for all code simplifies sharing data between the front end and back end, code reuse to accelerate development, and maintenance.

You can use Blazor to generate:

- Server-side code that handles UI interactions over a WebSocket connection.
- A client-side web app that runs directly in the browser via WebAssembly.

# What is WebAssembly?

WebAssembly (WASM) is an open binary standard. It defines a portable code format for programs designed to run in web browsers. WebAssembly is a textual assembly language with a compact binary format for fast downloads and near-native performance.

WebAssembly provides a compilation target for languages such as C, C++, and Rust. It's designed to run alongside JavaScript so that both work together. WebAssembly also can generate progressive web applications to be downloaded and run offline.

# What is Blazor WebAssembly?

With Blazor WebAssembly, developers can run .NET code in a browser. It's a single-page app framework that uses the WebAssembly open standards without requiring plug-ins or code generation.

.NET code executed via WebAssembly in a browser runs in the browser's JavaScript sandbox. The code includes all the security and protection that the sandbox provides. This inclusion helps prevent malicious actions on a client machine.

![WebAssembly](assets/blazor-webassembly.png)

Blazor uses a .NET runtime compiled to a WebAssembly module that is downloaded with an app. The module can execute .NET Standard code included in a Blazor app.

A Blazor WebAssembly app is restricted to the capabilities of the browser that executes the app. But the app can access full browser functionality via JavaScript interop.

# Blazor WebAssembly supported browsers

Blazor WebAssembly requires a modern desktop or mobile browser. The following browsers are currently supported:

- Microsoft Edge
- Mozilla Firefox
- Google Chrome
- Apple Safari

# What is Blazor Server?

Blazor Server provides support for hosting Razor components on the server in an ASP.NET Core app. UI updates are handled over a SignalR connection.

The runtime stays on the server and handles:

- Executing the app's C# code.
- Sending UI events from the browser to the server.
- Applying UI updates to the rendered components that are sent back by the server.

The connection used by Blazor Server to communicate with the browser is also used to handle JavaScript interop calls.

![server](assets/blazor-server.png)

# Blazor development requirements

You can build Blazor apps by using the latest version of Visual Studio 2022, Visual Studio for Mac, or Visual Studio Code. In this module, you'll use Visual Studio Code.

Whatever your development environment, you need to install the .NET 6.0 SDK. If you will be working with Visual Studio 2022, you will need to include the "ASP.NET and web development" workload to ensure the .NET 6.0 SDK and tools are available in Visual Studio. After installation, you'll have everything you need to start building Blazor apps. You'll build your first Blazor app with Visual Studio Code or Visual Studio 2022 in the next exercise.

# Creating the project

- Run the command `dotnet new blazorserver -f net6.0`
  - This command creates a basic Blazor server project with all required files and pages, along with a C# project file named `BlazorApp.csproj`.
- Run the app with `dotnet watch run`

# Razor Components

## What is Razor?

Razor is a markup syntax that uses HTML and C# for writing UI components of Blazor web apps.

Razor is based on ASP.NET and designed for creating web apps.

## What are Razor components?

A Razor file defines components that make up a portion of the app UI. Components in Blazor are analogous to user controls in ASP.NET Web Forms.

If you explore the project, you'll see that most files are .razor files.

At compile time, each Razor component is built into a .NET class. The class includes common UI elements like state, rendering logic, lifecycle methods, and event handlers.

# Quiz 1

1. Blazor App uses which run time?

   1. The runtime provided by the browser
   2. **The .NET runtime deployed with your web app**
      1. Blazor apps run in the browser or on the server on the .NET 5 runtime
   3. The JavaScript runtime deployed with your web app

2. How is Blazor UI defined?
   1. **As Razor pages with a mix of HTML and C#**
      1. A Razor file defines components that make up portions of UI for the app
   2. As XAML pages using XML
   3. In C# defined in .NET Standard libraries

# Data Binding and Events

You've defined the UI for your web app. Now explore how to add logic to the app. In a Blazor app, you can add C# code in separate .cs files or inline in your Razor components.

# C# code-behind in separate files

In Blazor, you can add C# files directly to your app project as with other .NET projects. Commonly called code-behind, this technique uses separate code files to store app logic. Separate files are a great strategy when your business logic is complex, is long, or has multiple classes.

For simple logic, you don't always need to create new .cs files.

# C# inline in components

A common practice is to mix HTML and C# in a single Razor component file. For simple components with lighter code requirements, this approach works well. To add code into a Razor file, you'll use directives.

# What are Razor directives?

Razor directives are component markup used to add C# inline with HTML. With directives, developers can define single statements, methods, or larger code blocks.

## Code Directives

Code directives should be familiar to developers who have used Razor in MVC or Pages.

You can use `@expression()` to add a C# statement inline with HTML. If you require more code, use the `@code` directive to add multiple statements enclosed by parentheses.

You can also add an `@functions` section to the template for methods and properties. They're added to the top of the generated class, where the document can reference them.

## Page Directive

The `@Page` directive is special markup that identifies a component as a page. Use this directive to specify a route. The route maps to an attribute route that the Blazor engine recognizes to register and access the page.

# Razor data binding

Within Razor components, you can data bind HTML elements to C# fields, properties, and Razor expression values. Data binding allows two-way synchronization between HTML and Microsoft .NET.

Data is pushed from HTML to .NET when a component is rendered. Components render themselves after event-handler code executes. That's why property updates are reflected in the UI immediately after an event handler is triggered.

Use `@bind` markup to bind a C# variable to an HTML object. You define the C# variable by name as a string in the HTML. You'll see an example of data binding in the following exercise.

# Create the ToDo Page

- Use the command ` dotnet new razorcomponent -n Todo -o Pages` to create a new component
- The `-n|--name` option in the preceding command specifies the name of the new Razor component. The new component is created in the project's Pages folder with the `-o|--output` option.

**Important**

Razor component file names require a capitalized first letter. Open the `Pages` folder and confirm that the `Todo` component file name starts with a capital letter T. The file name should be `Todo.razor`.

- Then add an `@page` directive with relative URL of `/todo`

- Add the Todo component to the navigation bar

  - The `NavMenu` component is used in the app's layout. Layouts are components that allow you to avoid duplication of content in an app. The `NavLink` component provides a cue in the app's UI when the component URL is loaded by the app.
  - In the `<nav>...</nav>` section of the `NavMenu` component, add the following new `<div>...</div>` and `NavLink` component for the Todo component.

- Create a Todo Item

  - Create a new file in the root of the project (the BlazorApp folder) named `TodoItem.cs` to hold a C# class that represents a todo item.

- Bind a list of TodoList Items

  - You're now ready to bind a collection of `TodoItem` objects to HTML in Blazor. We'll accomplish this by making the following changes in the `Pages/Todo.razor` file.
  - Add a field for the todo items in the @code block. The Todo component uses this field to maintain the state of the todo list.
  - Add unordered list markup and a foreach loop to render each todo item as a list item (<li>).

- Add Form Elements to Create Todos
  - The app requires UI elements for adding todo items to the list. Add a text input (`<input>`) and a button (`<button>`) below the unordered list (`<ul>...</ul>`)
  - When the Add todo button is selected, nothing happens because an event handler isn't attached to the button.
    - Add an AddTodo method to the Todo component and register the method for the button using the @onclick attribute. The AddTodo C# method is called when the button is selected
- To get the title of the new todo item, add a newTodo string field at the top of the `@code` block
- Modify the `<input>` element to bind newTodo with the `@bind` attribute
- Update the `AddTodo` method to add the `TodoItem` with the specified title to the list. Clear the value of the text input by setting newTodo to an empty string
- Save the `Pages/Todo.razor` file. The app is automatically rebuilt in the command shell. The page reloads in the browser after the browser reconnects to the app.
- The title text for each todo item can be made editable, and a checkbox can help the user keep track of completed items. Add a checkbox input for each todo item and bind its value to the `IsDone` property. Change `@todo.Title` to an `<input>` element bound to `todo.Title` with `@bind`
- Update the `<h3>` header to show a count of the number of todo items that aren't complete (`IsDone` is `false`).
