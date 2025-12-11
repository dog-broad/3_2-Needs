## 1. .NET vs C#

### 1.1 What is .NET, and what problems does it solve?

In an interview, you could say:

> .NET is a cross‑platform application development platform from Microsoft. It’s made up of a runtime, a large base class library, and tooling like the SDK and CLI. Its main goal is to let you build many kinds of applications—web, desktop, mobile, cloud—using a consistent programming model.
>
> It solves a few big problems:
> - It provides **managed execution**: garbage collection, type safety, exception handling.
> - It gives a rich **standard library** so you don’t constantly reinvent IO, networking, collections, serialization, etc.
> - It supports multiple languages (C#, F#, VB.NET) but they all run on the same runtime and share the same libraries.
> - And in modern .NET (like .NET 6/7/8), it’s **cross‑platform**, so the same code can run on Windows, Linux, and macOS.

Key interview points:
- “Runtime + libraries + tools”
- “Managed execution”
- “Cross‑platform, multi‑language, many app types”

---

### 1.2 What is C# and how is it related to .NET?

> C# is a modern, statically‑typed, object‑oriented programming language created by Microsoft. It’s the primary language used on the .NET platform.
>
> When I write C# code, the C# compiler compiles it to an intermediate language called IL. That IL runs on the .NET runtime (the CLR), which handles things like JIT compilation, garbage collection, and security.
>
> So I think of it like this:
> - **C#** is the language I write in.
> - **.NET** is the platform that runs the compiled code and gives me the libraries.

---

### 1.3 Difference between .NET Framework, .NET Core, and modern .NET (6/7/8)?

> Historically we had **.NET Framework**, which is the original, Windows‑only implementation. It’s still used in legacy enterprise apps, especially WinForms/WPF on Windows, but it’s mostly in maintenance.
>
> Then came **.NET Core**, which was a re‑implementation that is cross‑platform, open source, and much more modular and high‑performance.
>
> Starting with .NET 5, Microsoft **unified** the naming: now we just call it **.NET**, with versions like .NET 6, .NET 7, .NET 8. Those are the successors of .NET Core, not .NET Framework. They’re:
> - Cross‑platform.
> - Open source.
> - High‑performance (especially ASP.NET Core).
>
> For new projects, the guidance is to use the latest version of **modern .NET**, not .NET Framework.

---

### 1.4 What is the CLR? What does it do?

> The **CLR**, or Common Language Runtime, is the virtual machine component of .NET. It’s responsible for executing .NET code.
>
> Its main responsibilities are:
> - **JIT compilation**: it takes the IL produced by the C# compiler and compiles it to native machine code at runtime.
> - **Memory management** via the garbage collector.
> - **Type safety and security**, making sure code respects type rules and security boundaries.
> - **Exception handling** and stack unwinding.
> - **Threading and synchronization** primitives.
>
> Because of the CLR, different languages like C#, F#, and VB.NET can all compile to IL and run together in the same process.

---

### 1.5 What is IL (Intermediate Language)?

> IL is the CPU‑independent intermediate bytecode that C# (and other .NET languages) compile to.
>
> The workflow is:
> - You write C# → the C# compiler produces **IL** + metadata.
> - At runtime, the **JIT compiler in the CLR** turns IL into machine code for the specific CPU.
>
> This design gives us:
> - Language interoperability (all languages target IL).
        - Portability across architectures.
> - The ability for tools (like profilers, analyzers) to work at the IL level.

---

### 1.6 What is the Base Class Library (BCL)? Core namespaces?

> The Base Class Library, or BCL, is the set of core types and APIs that come with .NET. It’s like the “standard library.”
>
> It includes:
> - Fundamental types: `Object`, `String`, `Int32`, `DateTime`, etc.
> - Collections: `List<T>`, `Dictionary<TKey,TValue>`, arrays.
> - IO: file access, streams.
> - Networking: HTTP, sockets.
> - Threading and tasks: `Thread`, `Task`, async APIs.
>
> Common namespaces I use constantly:
> - `System` – basic types, exceptions, math, environment.
> - `System.Collections` and `System.Collections.Generic` – collections.
> - `System.Linq` – LINQ extension methods.
> - `System.IO` – files, directories, streams.
> - `System.Net`, `System.Net.Http` – networking.
> - `System.Threading`, `System.Threading.Tasks` – multithreading and async.

---

### 1.7 What types of applications can you build with .NET?

> .NET is very broad. With .NET I can build:
> - **Web APIs and web apps** using ASP.NET Core and Blazor.
> - **Desktop apps**: WPF and WinForms on Windows, and cross‑platform UIs using .NET MAUI.
> - **Cloud services and microservices**, often running in containers on Kubernetes, or in serverless environments like Azure Functions.
> - **Console tools and background workers**, for automation or scheduled jobs.
> - **Games and simulations** via engines like Unity (which uses C#).
> - IoT and even some embedded scenarios.
>
> So the same language (C#) and base libraries can be reused across multiple app types.

---

### 1.8 What are NuGet packages and how do you use them?

> NuGet is the package manager for .NET. A **NuGet package** is basically a compiled library plus metadata that you can consume in your project.
>
> I use NuGet to:
> - Bring in third‑party libraries (e.g. Serilog, AutoMapper, FluentValidation).
> - Reference Microsoft frameworks like EF Core providers, Azure SDKs.
>
> In practice:
> - From CLI: `dotnet add package PackageName`.
> - In Visual Studio: Manage NuGet Packages UI.
>
> When I build, the tooling automatically restores packages and adds them to the assembly references so I can `using` them in code.

---

## 2. C# Language Fundamentals

### 2.1 Explain value types vs reference types with examples.

> In C#, types are broadly divided into **value types** and **reference types**.
>
> **Value types**:
> - Typically stored on the stack or inline in other objects.
> - When you assign or pass them, they’re **copied by value**.
> - Examples: all the built‑in numeric types (`int`, `double`, `bool`), `struct`s and `enum`s.
>
> **Reference types**:
> - Live on the managed heap, and the variable holds a **reference** (pointer‑like) to that data.
> - When you assign or pass them, you copy the reference, so multiple variables can refer to the same object.
> - Examples: `string`, arrays, any `class` type, delegates.
>
> This distinction matters for performance and semantics. For example, modifying a value type copy doesn’t affect the original, but modifying a reference type via one variable is visible through other references.

---

### 2.2 Difference between `struct` and `class`?

> The main difference is that:
> - `class` is a **reference type**.
> - `struct` is a **value type**.
>
> Consequences:
> - Instances of a class are allocated on the heap and accessed by reference. Assigning a class variable copies the reference.
> - Instances of a struct are usually allocated on the stack or inline in other objects, and assigning them copies the whole value.
>
> Other differences:
> - Classes support inheritance; a class can inherit from another class.
> - Structs cannot inherit from another struct or class; they can only implement interfaces.
> - Structs are best for small, immutable data types where value semantics make sense (e.g. `DateTime`, `TimeSpan`, coordinate structs).
>
> In practice, most domain models are classes. Structs are used more for low‑level, performance‑critical, or small data types.

---

### 2.3 What is boxing and unboxing in C#?

> **Boxing** is the process of taking a value type and wrapping it in an object, so it can be treated as a reference type (`object` or an interface type). For example:
> ```csharp
> int x = 42;
> object o = x; // boxing
> ```
> The runtime allocates an object on the heap and copies the value into it.
>
> **Unboxing** is the reverse: extracting the value type from an object:
> ```csharp
> int y = (int)o; // unboxing
> ```
>
> Boxing/unboxing has a performance cost because it involves heap allocation and possibly copying, so in high‑performance or allocation‑sensitive code we try to avoid unnecessary boxing.

---

### 2.4 What are nullable types? `int?` vs `int`?

> Value types like `int` cannot be null by default; they always have some numeric value (default is 0).
>
> `int?` is shorthand for `Nullable<int>` and allows the variable to hold either a valid `int` or **null**, representing “no value.”
>
> This is especially useful when:
> - Mapping to database columns that can be NULL.
> - Representing optional values or “unknown” values.
>
> Example:
> ```csharp
> int? age = null;
> if (age.HasValue) { Console.WriteLine(age.Value); }
> ```
>
> With nullable value types we get explicit APIs like `.HasValue` and `.Value`, and they integrate nicely with operators.

---

### 2.5 What is the `var` keyword? Is C# dynamically typed when using `var`?

> `var` enables **implicit typing**. It tells the compiler, “infer the type from the right‑hand side.”
>
> For example:
> ```csharp
> var x = 10;         // x is int
> var name = "hello"; // name is string
> ```
>
> The important point: C# is still **statically typed**. The compiler determines the concrete type at compile time, and after that, `x` is an `int`, not an `object` or dynamic. You still get full type checking and IntelliSense.
>
> So using `var` does not make C# dynamically typed; it just reduces redundancy and keeps types in one place (usually on the right side).

---

### 2.6 Difference between `const` and `readonly`?

> Both are used to represent values that should not change, but they behave differently.
>
> **`const`**:
> - Must be assigned at declaration.
> - Value is baked into the compiled code at **compile time**.
> - Implicitly static.
> - Cannot be changed anywhere, even in a constructor.
>
> **`readonly` field**:
> - Can be assigned at declaration or in the constructor.
> - Value is fixed **per instance** (or per type if static readonly) after construction.
> - Not baked into the IL in the same way; can be evaluated at runtime.
>
> I use `const` for true constants (like pi approximation, string keys) and `readonly` for values that are constant after initialization but may depend on constructor arguments or configuration.

---

### 2.7 What is a namespace, and why do we use it?

> A namespace is a logical grouping of related types. It helps organize code and avoid name collisions.
>
> For example:
> ```csharp
> namespace MyCompany.MyProduct.Services
> {
>     public class OrderService { ... }
> }
> ```
>
> If another library also has an `OrderService`, the namespace distinguishes them. It also makes it easier to navigate and understand the structure of a large codebase.

---

### 2.8 Explain the `using` directive vs `using` for disposal.

> There are two different concepts that use the `using` keyword:
>
> 1. **`using` directive at the top of a file**:
>    - This imports a namespace so you can reference types without fully qualifying them.
>    - Example: `using System.Linq;`
>
> 2. **`using` statement / declaration for disposal**:
>    - This is for types that implement `IDisposable`. It guarantees that `Dispose()` is called when the scope ends, even if an exception occurs.
>    - Classic syntax:
>      ```csharp
>      using (var stream = File.OpenRead("file.txt"))
>      {
>          // use stream
>      } // Dispose is called here
>      ```
>    - Newer declaration syntax (C# 8+):
>      ```csharp
>      using var stream = File.OpenRead("file.txt");
>      // stream is disposed at the end of the scope
>      ```
>
> They’re completely different features that just share the same keyword.

---

### 2.9 What is the difference between `==` and `.Equals()` in C#?

> It depends on the type, but generally:
>
> - `==` is an **operator**. For many types it can be overloaded to have custom behavior.
> - `.Equals()` is a **virtual method** defined on `object` that types can override.
>
> For **value types**:
> - Both often compare the actual values.
>
> For **reference types**:
> - By default, `object`’s implementation of `==` compares references (are these two variables pointing to the same object?).
> - Many types like `string` overload `==` to compare contents, while also overriding `.Equals()` to do the same.
>
> When you implement your own types, you usually override `.Equals()` and `GetHashCode()`; and optionally you can overload `==` and `!=` to keep behavior consistent.

---

### 2.10 What are extension methods? How do you create one?

> Extension methods let me “add” new methods to an existing type **without modifying the original type** or using inheritance. They are syntactic sugar over static methods.
>
> To define an extension method:
> - Put it in a `static` class.
> - Mark the first parameter with the `this` keyword and the type you’re extending.
>
> Example:
> ```csharp
> public static class StringExtensions
> {
>     public static bool IsNullOrEmptyOrWhitespace(this string? value)
>     {
>         return string.IsNullOrWhiteSpace(value);
>     }
> }
>
> // Usage:
> string? name = "Alice";
> bool isEmpty = name.IsNullOrEmptyOrWhitespace();
> ```
>
> Under the hood, it’s still a static method call, but the syntax feels like you’re calling an instance method on the type.

---

## 3. OOP in C#

### 3.1 Explain the four pillars of OOP and how they apply in C#.

> The four pillars are **Encapsulation, Abstraction, Inheritance, and Polymorphism**.
>
> - **Encapsulation**:
>   - Grouping related data and behavior into classes, and hiding internal state using access modifiers.
>   - Example: a `BankAccount` class exposes `Deposit` and `Withdraw` methods, but the internal balance field is private.
>
> - **Abstraction**:
>   - Exposing only essential behavior, hiding implementation details.
>   - In C#, we use interfaces and abstract classes to express abstractions. For example, an `IRepository<T>` interface abstracts CRUD operations without exposing how they are implemented.
>
> - **Inheritance**:
>   - Creating new classes that reuse, extend, or modify behavior of existing classes.
>   - Example: `class Dog : Animal` inherits properties and behavior from `Animal`.
>
> - **Polymorphism**:
>   - The ability to treat different derived types through a common base interface and have them behave differently.
>   - In C#, achieved via virtual methods and interfaces:
>     ```csharp
>     Animal a = new Dog();
>     a.MakeSound(); // Dog's implementation is called
>     ```

---

### 3.2 What is an interface? How is it different from an abstract class?

> An **interface** defines a contract—basically, it says “any type that implements this must provide these members.” It contains method signatures, properties, etc., but no state. (Newer C# versions allow default implementations, but conceptually it’s still a contract.)
>
> An **abstract class**:
> - Can contain both abstract members (no implementation) and concrete members (with implementation).
> - Can have fields, constructors, protected members, and maintain state.
>
> Key differences:
> - A class can implement **multiple interfaces** but can inherit from only **one base class**.
> - Interfaces don’t have fields; abstract classes can.
> - Interfaces are generally used to define **capabilities/roles** that cut across different hierarchies, while abstract classes define a common base with shared implementation.

---

### 3.3 When would you use an abstract class vs an interface?

> I tend to use:
>
> - **Interfaces** when:
>   - I just need a contract, and I don’t care about shared implementation.
>   - I want to support multiple, unrelated object hierarchies.
>   - I care a lot about loose coupling and testability (mocking interfaces).
>
> - **Abstract classes** when:
>   - Types are closely related conceptually.
>   - I want to provide some base implementation or shared state.
>   - I expect to add new methods in the base later, and I don’t want to break all implementers (since changing an interface can be breaking).
>
> Example: For an application service, I’ll often define an interface like `IOrderService`. For a hierarchy of shapes, I might create an `abstract class Shape` with a virtual `Draw()` method and some common properties.

---

### 3.4 What does `virtual`, `override`, and `sealed` mean?

> These keywords control polymorphism and inheritance:
>
> - `virtual` on a base class method means:
>   - “This method has a default implementation, but derived classes are allowed to override it.”
>
> - `override` on a derived class method means:
>   - “I’m replacing the base class’s virtual method with my own implementation.”
>
> - `sealed` can be used on:
>   - A **class**: prevents further inheritance (`sealed class`).
>   - An **override method**: prevents that method from being overridden again in further derived classes.
>
> Example:
> ```csharp
> public class Animal
> {
>     public virtual void Speak() => Console.WriteLine("Some sound");
> }
>
> public class Dog : Animal
> {
>     public override void Speak() => Console.WriteLine("Woof");
> }
> ```

---

### 3.5 What is method overloading vs method overriding?

> - **Method overloading**:
>   - Same method name in the same class, but with different parameter lists (different types or counts).
>   - Resolved at **compile time**.
>   - Example: `void Log(string message)` and `void Log(string message, Exception ex)`.
>
> - **Method overriding**:
>   - A derived class provides a new implementation for a method defined as `virtual` in the base class.
>   - Resolved at **runtime** based on the actual type.
>   - Example: overriding `Speak()` in different animal subclasses.
>
> Overloading is compile‑time polymorphism; overriding is runtime polymorphism.

---

### 3.6 What is encapsulation in C#? How do access modifiers support it?

> Encapsulation is about **hiding internal state and implementation details** and exposing a clean public interface.
>
> Access modifiers in C# give us control over what’s visible:
> - `public`: accessible from anywhere.
> - `private`: only within the class itself.
> - `protected`: within the class and its derived classes.
> - `internal`: within the same assembly.
> - `protected internal`, `private protected`: combinations for specific scenarios.
>
> For example, I might keep a field `private` and expose a `public` property that enforces some validation, which is encapsulation in action.

---

### 3.7 What is a property in C#? How is it different from a field?

> A **field** is a simple variable declared inside a class or struct; it’s just storage.
>
> A **property** is a higher‑level construct that exposes getters and setters:
> ```csharp
> private string _name;
> public string Name
> {
>     get => _name;
>     set
>     {
>         if (string.IsNullOrWhiteSpace(value))
>             throw new ArgumentException("Name cannot be empty");
>         _name = value;
>     }
> }
> ```
>
> Properties let me:
> - Hide the underlying representation.
> - Add validation or side effects on get/set.
> - Still look like a simple field to consumers.
>
> In C#, best practice is to expose data via properties, not public fields.

---

### 3.8 What are auto‑implemented properties?

> Auto‑implemented properties are a shorthand when you don’t need extra logic:
> ```csharp
> public string Name { get; set; }
> ```
>
> The compiler automatically generates a hidden backing field. It’s equivalent to:
> ```csharp
> private string _name;
> public string Name
> {
>     get { return _name; }
>     set { _name = value; }
> }
> ```
>
> You can also make them read‑only or init‑only:
> ```csharp
> public string Name { get; init; } // C# 9+ init‑only setter
> ```

---

### 3.9 What is a static class / static member? When would you use it?

> A **static member** belongs to the type itself, not to any instance. You access it via the type:
> ```csharp
> Console.WriteLine(Math.PI);
> ```
>
> A **static class**:
> - Cannot be instantiated (no `new`).
> - Can only contain static members.
> - Typically used for utility or helper classes.
>
> Use cases:
> - Utility methods that don’t depend on instance state (`Math`, path helpers, etc.).
> - Global configuration/bootstrap code (sparingly).
>
> In many cases, especially for business logic, we prefer non‑static types so they can participate in DI and be mocked in tests.

---

### 3.10 What is a partial class? Why might you use it?

> A `partial` class allows the definition of a single class to be split across multiple files:
> ```csharp
> public partial class MyClass { /* part 1 */ }
> public partial class MyClass { /* part 2 */ }
> ```
>
> Common scenarios:
> - Tool‑generated code: e.g., code generators or designers generate part of a class, and you manually write additional members in another file without modifying generated code.
> - Very large classes (not ideal design, but sometimes necessary) where you separate concerns by file.
>
> It’s also used for partial records and partial interfaces.

---

## 4. Collections, Generics, LINQ

### 4.1 What are generics? Why are they useful?

> Generics allow you to define classes, interfaces, and methods with **type parameters**, so you can reuse the same logic for different types while keeping type safety.
>
> Example:
> - `List<int>` vs `List<string>` share the same implementation but are type‑safe.
>
> Benefits:
> - **Type safety**: you don’t need to cast from `object` and risk runtime errors.
> - **Performance**: avoids boxing/unboxing and casts.
> - **Reusability**: one generic implementation for many type scenarios.
>
> Generics are everywhere in .NET: collections, tasks (`Task<T>`), delegates (`Func<>`, `Action<>`), etc.

---

### 4.2 Explain `List<T>`, `Dictionary<TKey, TValue>`, `IEnumerable<T>`, `ICollection<T>`.

> - **`List<T>`**:
>   - A resizable, ordered list of items.
>   - Supports indexing (`list[0]`), adding/removing items, iteration.
>   - Backed by an array internally.
>
> - **`Dictionary<TKey, TValue>`**:
>   - Key‑value map with fast lookups by key (hash table).
>   - Keys must be unique.
>   - Great for scenarios where you frequently look up values by some identifier.
>
> - **`IEnumerable<T>`**:
>   - The most basic interface for a sequence of items you can enumerate with `foreach`.
>   - It’s read‑only (no add/remove), and it represents a sequence in general, including deferred sequences (like LINQ queries).
>
> - **`ICollection<T>`**:
>   - Extends `IEnumerable<T>`.
>   - Adds `Count`, `Add`, `Remove`, `Contains`, etc.
>   - Represents collections you can modify.
>
> So `List<T>` implements `IList<T>`, `ICollection<T>`, and `IEnumerable<T>`; `Dictionary<TKey, TValue>` implements applicable collection interfaces.

---

### 4.3 Difference between `IEnumerable<T>` and `IQueryable<T>`?

> - **`IEnumerable<T>`**:
>   - Represents an in‑memory sequence of items.
>   - LINQ operations on `IEnumerable<T>` are executed **in memory**.
>   - Great for working with collections already loaded in your process.
>
> - **`IQueryable<T>`**:
>   - Represents a query that can be translated into another query language (e.g., SQL).
>   - Used by ORMs like Entity Framework Core.
>   - LINQ expressions are translated into SQL and executed on the server; only results are materialized in memory.
>
> For example, `DbSet<T>` in EF Core implements `IQueryable<T>` so that your `Where`/`Select` operations are translated to SQL.

---

### 4.4 What is LINQ? Why is it powerful in C#?

> LINQ stands for **Language Integrated Query**. It’s a set of language features and APIs that let you query collections in a declarative, composable way, using C# syntax.
>
> Why it’s powerful:
> - Consistent query style across different data sources: in‑memory collections, XML, databases via LINQ to Entities.
> - Strongly typed: the compiler checks your queries and helps with IntelliSense.
> - Composable: you can chain operations (`Where`, `Select`, `OrderBy`, etc.) to build complex queries in a readable way.
>
> Example:
> ```csharp
> var adults = people
>     .Where(p => p.Age >= 18)
>     .OrderBy(p => p.LastName)
>     .Select(p => new { p.FirstName, p.LastName });
> ```

---

### 4.5 Difference between LINQ query syntax and method syntax?

> LINQ offers two syntaxes that are equivalent:
>
> - **Query syntax** (SQL‑like):
>   ```csharp
>   var result = from p in people
>                where p.Age >= 18
>                orderby p.LastName
>                select p;
>   ```
>
> - **Method syntax** (fluent, extension methods):
>   ```csharp
>   var result = people
>       .Where(p => p.Age >= 18)
>       .OrderBy(p => p.LastName)
>       .Select(p => p);
>   ```
>
> Under the hood, query syntax is translated into method calls. In practice, method syntax is more common, especially for more complex queries (joins, grouping).

---

### 4.6 Common LINQ operators and what they do.

Be ready to list and briefly define:

> - `Where` – filters a sequence based on a predicate.
> - `Select` – projects each element into a new form (transformation).
> - `OrderBy` / `OrderByDescending` – sorts a sequence by a key.
> - `GroupBy` – groups elements by a key.
> - `Join` – combines two sequences based on matching keys.
> - `Any` – returns true if **any** element matches a condition.
> - `All` – returns true if **all** elements match a condition.
> - `First` – returns the first element, throws if there is none.
> - `FirstOrDefault` – returns the first element or default (`null` for reference types) if there is none.
>
> Each operator returns another sequence or a scalar value, which makes them easy to chain.

---

### 4.7 What is deferred execution in LINQ?

> Many LINQ operators use **deferred execution**, which means:
> - They don’t actually run the query when you build the query expression.
> - They run when you **enumerate** the sequence: for example, in a `foreach` loop or when you call a terminal method like `ToList()` or `Count()`.
>
> This has two implications:
> - If the underlying collection changes before you enumerate, the query sees the updated data.
> - You can build queries in a modular way and only execute them once at the end.
>
> Methods like `ToList()`, `ToArray()`, `Count()`, `First()` trigger **immediate execution**.

---

### 4.8 What are anonymous types in C#? How are they often used with LINQ?

> Anonymous types are types without an explicit name, created using `new { ... }`.
>
> Example:
> ```csharp
> var personInfo = new { Name = "Alice", Age = 30 };
> Console.WriteLine(personInfo.Name);
> ```
>
> They’re commonly used in LINQ projections when you want to shape data:
> ```csharp
> var summary = people
>     .Select(p => new { p.Id, FullName = p.FirstName + " " + p.LastName });
> ```
>
> The compiler generates a type behind the scenes with read‑only properties for each initializer.

---

### 4.9 What is a delegate? How is it related to `Func<>` and `Action<>`?

> A **delegate** is a type‑safe function pointer: it encapsulates a method (or multiple methods) that can be called later.
>
> For example:
> ```csharp
> public delegate int Operation(int x, int y);
> ```
>
> `Func<>` and `Action<>` are built‑in generic delegate types:
> - `Func<T1, T2, TResult>` – represents a method that takes parameters and returns a value.
> - `Action<T1, T2>` – represents a method that takes parameters and returns void.
>
> Instead of defining custom delegates for every scenario, we typically use `Func<>` and `Action<>`. Lambdas are often assigned to these delegates.

---

### 4.10 What are lambda expressions? Give an example.

> A lambda expression is a concise way to write an anonymous function using the `=>` syntax.
>
> Example:
> ```csharp
> Func<int, int> square = x => x * x;
> var evens = numbers.Where(n => n % 2 == 0);
> ```
>
> Here:
> - `x => x * x` is a lambda that takes an `int` and returns its square.
> - `n => n % 2 == 0` is a lambda predicate used by `Where`.
>
> Lambdas are a key part of LINQ and functional‑style programming in C#.

---

## 5. Memory Management & Garbage Collection

### 5.1 How does memory management work in .NET?

> In .NET, memory management is **automatic** and handled by the CLR through managed memory and the garbage collector.
>
> Basic idea:
> - When I create objects, they are allocated on the managed heap.
> - I don’t explicitly free them. Instead, when objects are no longer reachable from any live references, the garbage collector eventually reclaims their memory.
> - The GC also compacts memory to reduce fragmentation.
>
> As a developer, I still need to be mindful of:
> - Holding references longer than necessary (can cause memory growth).
> - Disposing unmanaged resources (files, DB connections) via `IDisposable`.
>
> But I don’t call `free` or `delete` like in C++.

---

### 5.2 What is the garbage collector (GC)?

> The GC is a component of the CLR responsible for:
> - Finding objects that are no longer reachable.
> - Reclaiming their memory.
> - Compacting the heap to keep memory contiguous.
>
> .NET uses a **generational GC**:
> - Objects are grouped into generations (0, 1, 2) based on how long they’ve lived.
> - Most objects die young, so the GC optimizes by collecting Gen 0 frequently and higher generations less often.
>
> This design gives good performance in most real‑world scenarios without manual memory management.

---

### 5.3 What is the difference between managed and unmanaged resources?

> - **Managed resources** are things handled by the .NET runtime and garbage collector—normal objects on the managed heap.
> - **Unmanaged resources** are external resources not directly managed by the GC:
>   - File handles.
>   - Database connections.
>   - Network sockets.
>   - GDI handles, OS handles, etc.
>
> Even though the memory for the wrapper object is reclaimed by the GC, the **underlying OS resource** may need explicit cleanup, usually via `IDisposable` and `Dispose()`.

---

### 5.4 What is `IDisposable` and the Dispose pattern?

> `IDisposable` is an interface that defines a single method, `Dispose()`, intended to **release unmanaged resources** (and sometimes other expensive managed resources).
>
> The **Dispose pattern** typically:
> - Implements `IDisposable`.
> - Releases unmanaged resources in `Dispose()`.
> - Optionally implements a finalizer as a safety net.
> - Calls `GC.SuppressFinalize(this)` inside `Dispose()` to avoid running the finalizer if cleanup has already happened.
>
> Example pattern:
> ```csharp
> public class MyResource : IDisposable
> {
>     private bool _disposed;
>
>     public void Dispose()
>     {
>         Dispose(true);
>         GC.SuppressFinalize(this);
>     }
>
>     protected virtual void Dispose(bool disposing)
>     {
>         if (_disposed) return;
>
>         if (disposing)
>         {
>             // free managed resources
>         }
>
>         // free unmanaged resources
>         _disposed = true;
>     }
>
>     ~MyResource()
>     {
>         Dispose(false);
>     }
> }
> ```
>
> In user code, we rely on `using` to ensure `Dispose()` is called.

---

### 5.5 What is the `using` statement (for disposal), and why is it used?

> The `using` statement in this context is syntactic sugar around a `try/finally` that guarantees `Dispose()` is called.
>
> For example:
> ```csharp
> using (var connection = new SqlConnection(connString))
> {
>     connection.Open();
>     // use connection
> } // connection.Dispose() is called automatically
> ```
>
> This is important because it ensures that unmanaged resources like DB connections are released promptly, even if an exception is thrown. It helps prevent resource leaks (e.g., too many open connections).

---

### 5.6 What are finalizers (`~ClassName`) and when are they called?

> A **finalizer** (or destructor) is a special method that the GC calls **before** it reclaims an object’s memory. In C#, it looks like:
> ```csharp
> ~MyClass()
> {
>     // cleanup
> }
> ```
>
> Characteristics:
> - The timing is **non‑deterministic**—you don’t know exactly when it will run.
> - Finalizers are used as a **last resort** to clean up unmanaged resources if `Dispose()` wasn’t called.
> - They add overhead to garbage collection, so they should be used sparingly.
>
> The recommended pattern is: prefer `IDisposable` for deterministic cleanup; use finalizers only when you directly own unmanaged resources and need a safety net.

---

### 5.7 What are `stack` vs `heap` in the context of .NET memory?

> Conceptually:
>
> - **Stack**:
>   - Used for local variables, method call frames.
>   - Very fast allocation and deallocation (LIFO).
>   - Value types often live on the stack (though the compiler/JIT can optimize).
>
> - **Heap**:
>   - Used for objects and reference types.
>   - Managed by the garbage collector.
>   - Allocations are a bit more expensive but give us long‑lived data and flexible lifetimes.
>
> It’s a simplified mental model, but helpful for understanding performance: lots of small short‑lived allocations on the heap are cheap in .NET thanks to the generational GC, but keeping large graphs of objects alive unnecessarily can cause memory growth.

---

### 5.8 What are memory leaks in .NET? Can they still happen even with GC? Give examples.

> Even with GC, you can still have **logical memory leaks** if you keep references to objects longer than needed, so the GC can’t reclaim them.
>
> Examples:
> - **Static references**: a static collection that you keep adding to and never clear.
> - **Event handlers**: subscribing to events on long‑lived objects but never unsubscribing; the publisher holds references to subscribers, preventing their collection.
> - **Caches**: unbounded in‑memory caches that grow indefinitely.
> - **Unmanaged resources**: not calling `Dispose()` on things like large streams or DB connections, leading to resource exhaustion.
>
> So the GC protects against some classes of problems, but you still need to manage the **lifetime of references and unmanaged resources** carefully.
---

## 6. Exceptions & Error Handling

### 6.1 How does exception handling work in C#? Explain `try`, `catch`, `finally`.

> In C#, exceptions are the primary mechanism for handling error conditions. When something unexpected happens (like a failed cast, IO error, etc.), code can `throw` an exception, which unwinds the stack until it finds a matching `catch` block.
>
> The basic structure is:
> ```csharp
> try
> {
>     // Code that might throw
> }
> catch (SpecificException ex)
> {
>     // Handle specific error
> }
> catch (Exception ex)
> {
>     // Handle general error
> }
> finally
> {
>     // Cleanup code that must run regardless
> }
> ```
>
> - The `try` block contains code that might throw.
> - The `catch` blocks handle specific exceptions you expect and know how to recover from.
> - The `finally` block always runs—whether an exception was thrown or not—so it’s ideal for cleanup logic (closing files, releasing resources).

---

### 6.2 What’s the difference between checked and unchecked exceptions in C#?

> In C#, **all exceptions are unchecked**, which means:
> - The compiler doesn’t force you to declare which exceptions a method might throw.
> - It also doesn’t force callers to catch them.
>
> This is different from Java’s checked exceptions. In C#, you document exceptions and handle them by convention and good design, but the language doesn’t enforce catching or declaring them.

---

### 6.3 What are some common exception types in .NET?

You can list some typical ones and briefly describe:

> - `ArgumentException` / `ArgumentNullException` / `ArgumentOutOfRangeException` – thrown when a method receives invalid arguments.
> - `InvalidOperationException` – when an object’s current state doesn’t support the attempted operation.
> - `NullReferenceException` – when you try to dereference a `null` reference.
> - `FormatException` – when parsing fails (e.g., `int.Parse("abc")`).
> - `IndexOutOfRangeException` – accessing arrays or collections out of bounds.
> - `IOException` – general IO errors.
> - Database‑specific exceptions like `SqlException` from database drivers.

---

### 6.4 When would you create custom exception types?

> I create a custom exception type when:
> - I have a **domain‑specific error** that I want to distinguish from generic system errors.
> - I want callers to be able to **catch that specific error** and react accordingly.
>
> For example, in a payment system I might define a `PaymentFailedException` or `InsufficientFundsException`. That gives a clear, explicit signal and carries domain context (like an error code or extra details) in properties.

---

### 6.5 Why should you avoid catching general `Exception` in some scenarios?

> Catching `Exception` broadly can be dangerous because:
> - It may **swallow unexpected exceptions**, hiding bugs.
> - It may catch serious system exceptions (e.g., `OutOfMemoryException`, `StackOverflowException`), which you usually shouldn’t handle locally.
> - It makes debugging harder, because everything gets lumped into one handler.
>
> Best practice:
> - Catch **specific exceptions** you expect and can handle.
> - Use a **top‑level global handler** (e.g., middleware in ASP.NET Core) to log and return friendly error responses.
> - If you do catch `Exception`, usually rethrow or log and rethrow, unless you’re at a clearly defined boundary where you intentionally convert it into a specific, safe failure.

---

### 6.6 What is `throw` vs `throw ex` and why does it matter?

> Inside a `catch` block:
> - `throw;` rethrows the current exception while **preserving the original stack trace**.
> - `throw ex;` throws the same exception object but **resets the stack trace** to the current location, losing information about where it originally occurred.
>
> Because the stack trace is critical for debugging, you almost always want to use just `throw;` when you rethrow an exception after logging it.

---

## 7. Async / Await & Multithreading

### 7.1 What is a `Task` in .NET?

> A `Task` represents a **future operation** that may be running, completed, or faulted:
> - `Task` (no result) for operations that don’t return a value.
> - `Task<T>` for operations that return a value.
>
> It’s the core abstraction for asynchronous programming in .NET. You can `await` a `Task` to asynchronously wait for it to complete without blocking the thread.

---

### 7.2 Explain the `async` and `await` keywords. How do they work conceptually?

> The `async`/`await` pattern makes asynchronous code look like synchronous code.
>
> - `async` on a method:
>   - Allows the use of `await` inside.
>   - Typically changes the return type to `Task` or `Task<T>`.
>
> - `await`:
>   - Asynchronously waits for a `Task` to complete.
>   - The compiler rewrites the method into a **state machine**:
>     - It runs up to the first `await`.
>     - If the `Task` isn’t finished, it returns to the caller.
>     - When the `Task` completes, execution resumes after the `await`.
>
> Conceptually: `await` is a non‑blocking wait. It lets the thread go and resume later, rather than blocking the thread which would hurt scalability.

---

### 7.3 What is the difference between synchronous and asynchronous code?

> - **Synchronous** code:
>   - Each operation runs to completion before moving on.
>   - If you do IO (like a database call), the thread is blocked while waiting.
>
> - **Asynchronous** code:
>   - Operations that involve waiting (like IO) yield control when they’re waiting.
>   - The thread can do other work or return to the thread pool.
>   - Code resumes when the IO completes.
>
> In web applications, async code is especially important because it allows the server to handle more requests with the same number of threads, improving scalability.

---

### 7.4 Why is async I/O important in web applications?

> Web servers have a limited number of threads. If each incoming HTTP request performs blocking IO operations, those threads sit idle waiting for external resources (DB, HTTP calls).
>
> With async I/O:
> - While a request is waiting for a DB or external API, the thread can be released back to the pool.
> - That thread can then serve another request.
>
> This improves:
> - **Throughput** (more requests per second).
> - **Resource utilization**.
> - Overall scalability, especially under high load where lots of requests are waiting on IO.

---

### 7.5 What does “don’t block on async code” mean? Why are `.Result` / `.Wait()` dangerous?

> “Don’t block on async code” means:
> - If you start using async/await, you should **stay async all the way up** to the top of the call stack (e.g., the controller action).
> - Avoid calling `.Result`, `.Wait()`, or `.GetAwaiter().GetResult()` on a `Task`.
>
> Blocking on tasks can cause:
> - **Deadlocks** in environments with a synchronization context (older ASP.NET, WinForms, WPF), because the continuation tries to run on a thread that is blocked waiting for the result.
> - **Thread starvation** and reduced scalability.
>
> Best practice: make the calling method async too and `await` the task instead of blocking.

---

### 7.6 What is `Task.Run` and when should you use/not use it?

> `Task.Run` schedules a piece of work to run on a thread pool thread:
> ```csharp
> Task.Run(() => { /* CPU-bound work */ });
> ```
>
> It’s appropriate when:
> - You have **CPU‑bound** work in a UI or request thread and want to offload it to the background to keep the UI responsive or free the request thread.
>
> It’s **not** appropriate for:
> - Pure IO‑bound operations that already have async APIs (like `HttpClient.GetAsync`, `DbContext` async methods). Wrapping those in `Task.Run` just adds unnecessary overhead and doesn’t improve scalability.

---

### 7.7 What is a deadlock? Async scenario example.

> A deadlock is a situation where two operations wait on each other, so neither can proceed.
>
> Classic async deadlock example:
> - You have an async method:
>   ```csharp
>   public async Task FooAsync()
>   {
>       await SomeAsyncOperation();
>   }
>   ```
> - On the main/UI thread, you call:
>   ```csharp
>   FooAsync().Result; // or .Wait()
>   ```
> - The `await` inside `FooAsync` tries to resume on the **captured synchronization context** (e.g., UI thread), but that thread is blocked on `.Result`.
> - So the awaited operation can’t complete, and `.Result` never returns → deadlock.
>
> Solution: avoid blocking on tasks, and use `await` instead.

---

### 7.8 What is `ConfigureAwait(false)` and where is it typically used?

> `ConfigureAwait(false)` tells the awaiter **not** to capture the current synchronization context:
> ```csharp
> await SomeTask.ConfigureAwait(false);
> ```
>
> Meaning:
> - After the awaited task completes, the continuation can run on **any thread**, not necessarily the original context (like the UI thread).
>
> It’s typically used:
> - In **library code** where you don’t care about resuming on the original context.
> - In server‑side code (like ASP.NET Core), where there’s usually no UI context, to avoid some overhead.
>
> In modern ASP.NET Core, you often don’t need `ConfigureAwait(false)` because there’s no synchronization context by default, but it’s still a common pattern in shared libraries.

---

### 7.9 What is the thread pool? How does .NET use it?

> The thread pool is a pool of worker threads managed by the CLR:
> - It maintains a collection of reusable threads.
> - It grows and shrinks based on workload.
>
> The .NET runtime uses the thread pool for:
> - Executing asynchronous continuations.
> - Handling tasks scheduled with `Task.Run`.
> - Timer callbacks, IO completion, `ThreadPool.QueueUserWorkItem`, etc.
>
> Using the thread pool avoids creating and destroying threads constantly, which is expensive.

---

### 7.10 Difference between parallelism (e.g., `Parallel.ForEach`) and asynchrony?

> **Parallelism**:
> - About doing **multiple CPU‑bound tasks at the same time** using multiple cores.
> - `Parallel.ForEach` splits work across multiple threads to complete faster.
>
> **Asynchrony**:
> - About **non‑blocking waiting**, primarily for IO‑bound operations.
> - Async/await frees the thread while the operation is waiting on external resources.
>
> You can have:
> - Asynchronous **but single‑threaded** IO (e.g., one request, one thread, but not blocked).
> - Parallel **CPU‑bound** work using multiple threads.
>
> Both can be combined when appropriate, but they solve different problems.

---

## 8. ASP.NET Core & Web APIs

### 8.1 What is ASP.NET Core? How is it different from older ASP.NET?

> ASP.NET Core is the modern, cross‑platform, open‑source web framework in the .NET ecosystem. It’s designed for:
> - High performance.
> - Cross‑platform (Windows, Linux, macOS).
> - Modularity and composability.
>
> Compared to older ASP.NET (System.Web):
> - ASP.NET Core has a **lightweight middleware pipeline** instead of the old HTTP modules/handlers.
> - Built‑in dependency injection from day one.
> - Unified hosting model and configuration system.
> - No direct dependency on IIS; it uses Kestrel and can be hosted self‑contained or behind reverse proxies (IIS, Nginx, etc.).
>
> For new web/API projects, ASP.NET Core is the recommended choice.

---

### 8.2 Explain middleware in ASP.NET Core.

> Middleware are components that **participate in the HTTP request/response pipeline**. Each middleware:
> - Receives the HTTP context.
> - Can do some work (logging, auth, modifying headers, etc.).
> - Optionally calls the next middleware in the pipeline.
>
> The pipeline is defined in code, usually in `Program.cs`:
> ```csharp
> app.UseRouting();
> app.UseAuthentication();
> app.UseAuthorization();
> app.UseEndpoints(...);
> ```
>
> The order of middleware is crucial. For example, authentication must run before authorization, and routing must occur before endpoint execution.

---

### 8.3 How does the request pipeline work in ASP.NET Core?

> The request pipeline is an ordered chain of middleware. For a typical app:
> 1. Request enters Kestrel (web server).
> 2. It passes through global middlewares (e.g., exception handling, logging, CORS).
> 3. `UseRouting` determines which endpoint should handle the request.
> 4. `UseAuthentication` authenticates the user and sets `HttpContext.User`.
> 5. `UseAuthorization` enforces authorization policies.
> 6. The endpoint is executed (controller action or minimal API handler).
> 7. The response flows back through the middleware chain on the way out.
>
> Each middleware can read/modify the request and response and decide whether to short‑circuit the pipeline.

---

### 8.4 What is a minimal API vs MVC controller?

> - **Minimal APIs**:
>   - Introduced in .NET 6.
>   - Lightweight way to build HTTP APIs with minimal ceremony.
>   - Define routes and handlers directly in `Program.cs`:
>     ```csharp
>     app.MapGet("/hello", () => "Hello");
>     ```
>   - Great for small services, prototypes, microservices.
>
> - **MVC controllers**:
>   - More structured approach using controllers and attributes:
>     ```csharp
>     [ApiController]
>     [Route("api/[controller]")]
>     public class ProductsController : ControllerBase
>     {
>         [HttpGet("{id}")]
>         public IActionResult Get(int id) { ... }
>     }
>     ```
>   - Better for larger applications where you want clear separation, filters, and rich features.

---

### 8.5 How do you define and route HTTP endpoints?

> With **minimal APIs**:
> ```csharp
> app.MapGet("/todos", () => ...);
> app.MapPost("/todos", (Todo todo) => ...);
> app.MapDelete("/todos/{id}", (int id) => ...);
> ```
>
> With **MVC controllers**:
> ```csharp
> [ApiController]
> [Route("api/[controller]")]
> public class TodosController : ControllerBase
> {
>     [HttpGet]
>     public IActionResult GetAll() { ... }
>
>     [HttpGet("{id}")]
>     public IActionResult Get(int id) { ... }
>
>     [HttpPost]
>     public IActionResult Create(Todo dto) { ... }
> }
> ```
>
> Routing is configured with `UseRouting()` and `UseEndpoints()` or `MapControllers()`.

---

### 8.6 What is model binding and model validation?

> **Model binding**:
> - ASP.NET Core automatically maps HTTP request data (route values, query string, headers, body) to action parameters or model objects.
> - For example, if your action parameter is `TodoCreateDto dto`, the framework will read JSON from the body and populate that object.
>
> **Model validation**:
> - Uses data annotations and validation attributes on your model:
>   ```csharp
>   public class TodoCreateDto
>   {
>       [Required]
>       public string Title { get; set; }
>
>       [Range(1, 5)]
>       public int Priority { get; set; }
>   }
>   ```
> - The framework validates the model after binding. If invalid, you can check `ModelState.IsValid` or let `[ApiController]` attribute automatically return a 400 response with validation details.

---

### 8.7 How do you return appropriate HTTP status codes from an API?

> In MVC controllers, I typically return `IActionResult` or specific result types:
> ```csharp
> return Ok(data);             // 200
> return Created(uri, data);   // 201
> return NoContent();          // 204
> return BadRequest(error);    // 400
> return NotFound();           // 404
> return StatusCode(500);      // 500
> ```
>
> In minimal APIs, I can:
> - Return raw types (which serialize to JSON) and let the framework default to 200.
> - Use `Results` helpers:
>   ```csharp
>   return Results.Ok(data);
>   return Results.NotFound();
>   ```
>
> The key is to match the response status code to the outcome of the operation (success vs validation error vs not found vs server error).

---

### 8.8 What are filters in ASP.NET Core (e.g., action filters, exception filters)?

> Filters are a way to run code before or after certain parts of the MVC pipeline:
> - **Action filters** – run before and/or after an action method.
> - **Authorization filters** – run before anything else to enforce security.
> - **Exception filters** – catch unhandled exceptions thrown by actions and translate them into consistent responses.
> - **Result filters** – run before/after the action result is executed (for response shaping).
>
> They’re useful for cross‑cutting concerns such as logging, caching, auditing, and global exception handling.

---

### 8.9 How is dependency injection integrated into ASP.NET Core?

> ASP.NET Core has DI built‑in:
> - There is a **service container** (`IServiceCollection`) where you register services in `Program.cs`:
>   ```csharp
>   builder.Services.AddScoped<IOrderService, OrderService>();
>   ```
> - Framework components like controllers, minimal API handlers, and middlewares can request dependencies via **constructor parameters** or method parameters (for minimal APIs).
> - When a request comes in, the framework creates a **scope** and resolves scoped services from the container, injecting them wherever needed.
>
> This makes it very natural to write testable, loosely coupled code.

---

### 8.10 How do you handle configuration in ASP.NET Core (appsettings.json, env vars)?

> ASP.NET Core uses a flexible configuration system:
> - It reads configuration from multiple sources:
>   - `appsettings.json`.
>   - `appsettings.{Environment}.json`.
>   - Environment variables.
>   - User secrets (in development).
>   - Command‑line arguments.
>
> In code:
> - You can inject `IConfiguration` where needed.
> - Or bind sections to strongly typed options:
>   ```csharp
>   builder.Services.Configure<MyOptions>(
>       builder.Configuration.GetSection("MyOptions"));
>   ```
> - Then inject `IOptions<MyOptions>` or `IOptionsSnapshot<MyOptions>` in your services.
>
> This setup allows you to vary configuration per environment without changing code.

---

### 8.11 What is middleware like `UseRouting`, `UseAuthentication`, `UseAuthorization`?

> These are key middleware components:
> - `UseRouting` – matches the request path and HTTP method to an endpoint (like a controller action or minimal API).
> - `UseAuthentication` – reads authentication tokens (like JWTs, cookies), validates them, and sets `HttpContext.User`.
> - `UseAuthorization` – enforces the authorization policies and roles for the current user.
>
> Order matters:
> - `UseRouting()` → `UseAuthentication()` → `UseAuthorization()` → endpoints is the typical sequence.

---

### 8.12 How do you handle cross‑origin requests (CORS)?

> CORS (Cross‑Origin Resource Sharing) controls which front‑end origins can call your API from a browser.
>
> In ASP.NET Core:
> - You define a CORS policy:
>   ```csharp
>   builder.Services.AddCors(options =>
>   {
>       options.AddPolicy("MyPolicy", policy =>
>           policy.WithOrigins("https://myfrontend.com")
>                 .AllowAnyHeader()
>                 .AllowAnyMethod());
>   });
>   ```
> - Then apply it:
>   ```csharp
>   app.UseCors("MyPolicy");
>   ```
> - Or decorate controllers/actions with `[EnableCors("MyPolicy")]`.
>
> This ensures browsers enforce your configured cross‑origin rules.

---

## 9. Dependency Injection & Architecture

### 9.1 What is dependency injection (DI)? Why is it useful?

> DI is a design pattern where a class’s dependencies are **provided to it from the outside** rather than created internally. Instead of `new`ing up dependencies inside your classes, you request abstractions in your constructor.
>
> It’s useful because:
> - It **decouples** classes from specific implementations.
> - Makes code **more testable** (you can pass mocks or stubs).
> - Centralizes object creation and lifetime via a container.
> - Encourages better design with clear dependencies.

---

### 9.2 Constructor injection, property injection, method injection.

> - **Constructor injection**:
>   - Dependencies are passed via the constructor.
>   - It’s the most common and recommended form in ASP.NET Core.
>   ```csharp
>   public class OrderService
>   {
>       private readonly IRepository _repo;
>       public OrderService(IRepository repo)
>       {
>           _repo = repo;
>       }
>   }
>   ```
>
> - **Property injection**:
>   - Dependencies are assigned to public settable properties.
>   - Useful in some limited scenarios but less explicit than constructor injection.
>
> - **Method injection**:
>   - Dependencies are passed as parameters to individual methods.
>   - Useful for optional dependencies or when dependency is only needed in specific methods.

---

### 9.3 Difference between `AddSingleton`, `AddScoped`, and `AddTransient` lifetimes?

> In ASP.NET Core DI:
> - `AddSingleton`:
>   - One instance for the entire application lifetime.
>   - Good for stateless services, configuration providers, etc.
>
> - `AddScoped`:
>   - One instance per **scope**, which in web apps typically means per HTTP request.
>   - Good for services that represent a unit of work, like a `DbContext`.
>
> - `AddTransient`:
>   - A new instance each time it’s requested from the container.
>   - Good for lightweight, stateless services with no shared state.

---

### 9.4 What problems does DI solve in a typical application?

> DI mainly solves:
> - **Tight coupling** between classes and concrete implementations.
> - Difficulty in testing because classes create their own dependencies.
> - Spaghetti object creation logic spread throughout the codebase.
>
> With DI:
> - You can inject different implementations (e.g., real vs mock) based on environment.
> - Your business logic classes are focused on behavior, not object construction.
> - You can wire up dependencies in one place (startup/Program).

---

### 9.5 Can you explain inversion of control (IoC)?

> Inversion of control is a broader principle where the control of object creation and flow is inverted:
> - Instead of your code manually instantiating and orchestrating everything, you rely on a framework or container to do it.
>
> In the DI context:
> - The IoC container is responsible for:
>   - Creating instances.
>   - Resolving dependencies.
>   - Managing lifetimes.
>
> Your classes just declare what they need, and the container supplies it.

---

### 9.6 What is a service container / IoC container?

> A service container (IoC container) is:
> - A component that holds registrations of **services** (interfaces and their implementations) and their lifetimes.
> - When asked, it creates instances, resolves dependencies, and caches them according to lifetime rules.
>
> In ASP.NET Core:
> - `IServiceCollection` is used to configure services at startup.
> - `IServiceProvider` is the runtime container that actually resolves them.

---

### 9.7 What is SOLID? Briefly describe each principle.

Use a short, clear explanation of each:

> - **S – Single Responsibility Principle**:
>   - A class should have one reason to change, i.e., one responsibility.
>
> - **O – Open/Closed Principle**:
>   - Classes should be open for extension but closed for modification.
>   - Use abstractions and composition so you can extend behavior without changing existing code.
>
> - **L – Liskov Substitution Principle**:
>   - Subtypes must be substitutable for their base types without breaking correctness.
>
> - **I – Interface Segregation Principle**:
>   - Prefer many small, specific interfaces over one large, “fat” interface.
>
> - **D – Dependency Inversion Principle**:
>   - High‑level modules should not depend on low‑level modules; both should depend on abstractions.
>   - Abstractions should not depend on details; details depend on abstractions.

---

### 9.8 How would you structure a typical .NET solution (API, Application, Domain, Infrastructure)?

> A common clean architecture style for a .NET app:
>
> - **Domain layer**:
>   - Contains domain entities, value objects, domain services, and business rules.
>   - Has no dependencies on other layers.
>
> - **Application layer**:
>   - Contains use cases, application services, DTOs, interfaces for persistence or external services.
>   - Depends on Domain but not on Infrastructure.
>
> - **Infrastructure layer**:
>   - Contains EF Core DbContexts, repositories, external service implementations, file IO, email senders, etc.
>   - Implements interfaces defined in the Application layer.
>
> - **API/Presentation layer**:
>   - ASP.NET Core project with controllers or minimal APIs.
>   - Handles HTTP, maps requests to application use cases, and converts results to HTTP responses.
>
> This separation:
> - Keeps business logic independent of infrastructure details.
> - Makes the core easier to test and maintain.

---

## 10. Entity Framework Core / Data Access

### 10.1 What is Entity Framework Core (EF Core)?

> EF Core is Microsoft’s modern **Object‑Relational Mapper (ORM)** for .NET:
> - It maps C# classes (entities) to database tables.
> - Lets you write queries using LINQ instead of raw SQL.
> - Handles change tracking, insert/update/delete operations, and migrations.
>
> It supports multiple database providers (SQL Server, PostgreSQL, MySQL, SQLite, etc.).

---

### 10.2 What is Code‑First vs Database‑First development?

> - **Code‑First**:
>   - You start by modeling your domain entities in C#.
>   - EF Core can create and evolve the database schema from your models using **migrations**.
>   - Very common in greenfield projects and domain‑driven design.
>
> - **Database‑First**:
>   - You start with an existing database schema.
>   - You generate C# models from the database (scaffolding).
>   - More common when integrating with an established database you don’t control.

---

### 10.3 What is a `DbContext` and a `DbSet<T>`?

> - `DbContext`:
>   - The main class that represents a **session with the database**.
>   - Manages entity objects during runtime, including change tracking and saving to the database.
>   - Configured with connection string and options.
>
> - `DbSet<T>`:
>   - Represents a table or collection of entities of type `T`:
>     ```csharp
>     public DbSet<Customer> Customers { get; set; }
>     ```
>   - Provides methods for querying and saving instances of `T`.
>   - Under the hood, implements `IQueryable<T>` so you can build LINQ queries that translate to SQL.

---

### 10.4 What are migrations in EF Core?

> Migrations are EF Core’s way of tracking and applying schema changes over time.
>
> With Code‑First:
> - When you change your model, you create a **migration**:
>   ```bash
>   dotnet ef migrations add AddCustomerTable
>   ```
> - This generates C# code that describes how to apply (and roll back) schema changes.
> - You then apply migrations to the database:
>   ```bash
>   dotnet ef database update
>   ```
>
> Benefits:
> - Versioned, scriptable schema evolution.
> - Keep code and database in sync.

---

### 10.5 How do you configure relationships (one‑to‑many, many‑to‑many) in EF Core?

> Relationships are configured using:
> - Conventions (naming, navigation properties).
> - Data annotations (`[ForeignKey]`, etc.).
> - Fluent API in `OnModelCreating`.
>
> Example: one‑to‑many:
> ```csharp
> modelBuilder.Entity<Order>()
>     .HasOne(o => o.Customer)
>     .WithMany(c => c.Orders)
>     .HasForeignKey(o => o.CustomerId);
> ```
>
> Example: many‑to‑many (EF Core 5+ supports skip navigations):
> ```csharp
> modelBuilder.Entity<Student>()
>     .HasMany(s => s.Courses)
>     .WithMany(c => c.Students);
> ```

---

### 10.6 What is lazy loading, eager loading, and explicit loading?

> These refer to when related data (navigation properties) is loaded:
>
> - **Lazy loading**:
>   - Related data is loaded **on first access** of the navigation property.
>   - Requires configuration (proxies or manual patterns).
>   - Can lead to N+1 queries if not careful.
>
> - **Eager loading**:
>   - You specify related data to load as part of the initial query using `Include`:
>   ```csharp
>   var orders = context.Orders
>       .Include(o => o.Customer)
>       .ToList();
>   ```
>   - Good when you know you’ll need related data.
>
> - **Explicit loading**:
>   - You load related data on demand using the context:
>   ```csharp
>   context.Entry(order).Collection(o => o.OrderLines).Load();
>   ```
>
> Making the right choice affects performance and number of queries.

---

### 10.7 What is `AsNoTracking()` and why might you use it?

> `AsNoTracking()` tells EF Core **not to track** the returned entities in the change tracker:
> ```csharp
> var customers = context.Customers.AsNoTracking().ToList();
> ```
>
> Benefits:
> - Lower memory usage.
> - Better performance for read‑only scenarios, because EF doesn’t track changes.
>
> I use it when:
> - I’m building read‑only queries (e.g., for reporting, or read‑only APIs).
> - I don’t plan to modify the entities and call `SaveChanges()` on them.

---

### 10.8 How do you handle transactions in EF Core?

> By default, `SaveChanges()` wraps operations in a transaction if needed. For more control:
>
> - Manually create and manage a transaction:
> ```csharp
> using var transaction = await context.Database.BeginTransactionAsync();
> // Execute multiple operations that should be atomic
> await context.SaveChangesAsync();
> await transaction.CommitAsync();
> ```
>
> - Or use ambient transactions (`TransactionScope`) in some scenarios.
>
> The key is to ensure that sets of operations that must succeed or fail together are wrapped in a single transaction.

---

### 10.9 What are common performance pitfalls with EF Core?

Mention a few concrete pitfalls:

> - N+1 queries due to unplanned lazy loading.
> - Not using `AsNoTracking` for read‑only queries, causing unnecessary tracking overhead.
> - Loading too much data at once (no pagination, no `Take`/`Skip`).
> - Doing heavy logic inside LINQ queries that cannot translate to SQL, causing client‑side evaluation (depending on EF Core version and configuration).
> - Chatty database access (many small queries in loops instead of batch operations).
>
> Mitigations:
> - Use `Include` strategically.
> - Profile generated SQL.
> - Use pagination (`Skip`, `Take`).
> - Consider projections (`Select`) to load only needed columns.

---

## 11. Practical / Scenario‑Based Questions

For these, you should adapt answers to your real experience. I’ll give strong templates.

### 11.1 Describe a project you built with .NET/C#. What was your role and what technologies did you use?

Structure with **context → your role → tech → results**:

> In my last project, I worked on a [type of system, e.g., “order management API”] for [company/client type]. The goal was to [short business goal: e.g., “allow internal systems to place and track orders”].
>
> We built the backend using **ASP.NET Core** (for REST APIs) and **Entity Framework Core** with [SQL Server/PostgreSQL] as the database. We used **[DI, AutoMapper, FluentValidation, xUnit]** etc.
>
> My role was [e.g., “backend developer”], and I was responsible for:
> - Designing and implementing API endpoints (CRUD, search, etc.).
> - Modeling entities and relationships in EF Core.
> - Writing unit and integration tests to cover key scenarios.
> - Participating in code reviews and improving performance in some heavy queries.
>
> We successfully [brief result: e.g., “deployed the system to production and reduced manual processing time by X%”].

---

### 11.2 How do you structure a new .NET application from scratch?

> When I start a new .NET application, I usually:
> 1. Clarify the **requirements and architecture**: is it a web API, full‑stack app, microservice, etc.?
> 2. Create a solution with **logical projects/layers**:
>    - API/Presentation (ASP.NET Core project).
>    - Application layer (use cases, DTOs).
>    - Domain layer (entities, domain services).
>    - Infrastructure layer (EF Core, repositories, external integrations).
> 3. Define the **domain model** and core entities.
> 4. Set up **EF Core** (if using a relational DB), configure DbContext and migrations.
> 5. Configure **DI**, **logging**, and **configuration** (appsettings, environment‑specific files).
> 6. Implement the first vertical slice: from controller endpoint → application service → domain → persistence, with tests.
> 7. Iterate, adding features while maintaining separation of concerns and consistent patterns.

---

### 11.3 How would you design a simple REST API for a to‑do list?

> For a simple to‑do API, I’d:
> - Define the main **resource**: `TodoItem` with fields like `Id`, `Title`, `IsCompleted`, `DueDate`.
> - Design endpoints:
>   - `GET /api/todos` – list all items, optionally filtered.
>   - `GET /api/todos/{id}` – get a single item.
>   - `POST /api/todos` – create a new item.
>   - `PUT /api/todos/{id}` or `PATCH` – update an item.
>   - `DELETE /api/todos/{id}` – delete an item.
> - Use **DTOs** for input/output, with validation attributes (e.g., `[Required]`).
> - Use **EF Core** to persist to a database, or an in‑memory store for a very simple version.
> - Return appropriate HTTP codes (201 for create, 404 for not found, 400 for validation errors).
> - Add basic logging and error handling (global exception handler).

---

### 11.4 How would you log and handle errors in a production ASP.NET Core app?

> For logging and error handling, I usually:
> - Use the built‑in **logging abstractions** (`ILogger`) and configure providers (console, file, Application Insights, etc.).
> - Implement **global exception handling**:
>   - In ASP.NET Core, I can use the built‑in Developer Exception Page in dev.
>   - In production, I configure a custom exception‑handling middleware that:
>     - Logs the exception with context.
>     - Returns a consistent error response (e.g., RFC 7807 “Problem Details” JSON) without leaking internal details.
> - Use structured logging (log properties rather than just strings) to make searching easier.
> - Ensure logs include correlation IDs or trace IDs to follow a request across services.

---

### 11.5 How would you secure an API (high level)?

> At a high level, to secure an API:
> - Use **HTTPS** everywhere to protect data in transit.
> - Implement **authentication**:
>   - Commonly via JWT bearer tokens issued by an Identity Provider (e.g., IdentityServer, Azure AD, Auth0).
> - Implement **authorization**:
>   - Use roles/claims and ASP.NET Core authorization policies to restrict access to certain endpoints.
> - Validate and sanitize inputs to avoid injection attacks.
> - Protect against common vulnerabilities (rate limiting, CSRF for browser‑based flows where needed, etc.).
> - Store secrets (connection strings, API keys) securely (user secrets in dev, Key Vault in production).

---

### 11.6 How do you test your .NET code? Which frameworks have you used?

> I typically write tests at multiple levels:
> - **Unit tests**:
>   - Focused on individual classes or methods.
>   - Use frameworks like **xUnit** or **NUnit**.
>   - Use mocking libraries such as Moq to mock dependencies (e.g., repositories or external services).
> - **Integration tests**:
>   - Test components working together, like API + DB.
>   - ASP.NET Core provides `WebApplicationFactory` to host an in‑memory server and send HTTP requests.
> - Optionally, **end‑to‑end tests** for UI or more complex flows.
>
> I run tests locally and in CI pipelines to catch regressions early.

---

### 11.7 How do you handle configuration per environment (dev, test, prod)?

> I rely on ASP.NET Core’s configuration system:
> - Use `appsettings.json` for defaults.
> - Override with `appsettings.Development.json`, `appsettings.Production.json`, etc., based on `ASPNETCORE_ENVIRONMENT`.
> - Use **environment variables** to override specific values, especially in containers/CI.
> - Use **User Secrets** in development for sensitive values like connection strings and API keys.
> - In production, use a secure secret store like Azure Key Vault.
>
> This way, the same codebase can run in different environments with environment‑specific settings without code changes.

---

### 11.8 Explain a bug you faced in C#/.NET and how you debugged/fixed it.

Use the STAR format (Situation, Task, Action, Result). For example:

> We had an issue where a certain API endpoint started timing out under load.
> - **Situation**: Under normal conditions it was fine, but during peak load, response times spiked and sometimes timed out.
> - **Task**: My task was to identify the bottleneck and fix it.
> - **Action**:
>   - I enabled detailed logging and added timing around different parts of the code.
>   - I used a profiler / logging to see that most time was spent in database queries.
>   - Inspecting EF Core logs, I noticed multiple small queries inside a loop—classic N+1 problem.
>   - I refactored the code to use a single query with `Include` and proper filtering.
> - **Result**:
>   - After deployment, the endpoint’s latency decreased significantly and timeouts disappeared under the same load.
>
> This experience reinforced for me the importance of profiling and understanding how ORMs translate LINQ to SQL.

---

## 12. C# Versions & Newer Features

### 12.1 What features were introduced in recent C# versions that you use often?

You can pick a few and describe briefly, e.g.:

> Some recent C# features I find very useful:
> - **Nullable reference types (C# 8)** – helps avoid null reference exceptions by making nullability explicit in the type system.
> - **Switch expressions and enhanced pattern matching (C# 8/9)** – more expressive, concise branching logic.
> - **Records (C# 9)** – concise syntax for immutable data types with value‑based equality, great for DTOs.
> - **Top‑level statements (C# 9)** – simplify console app boilerplate.
> - **Global using directives (C# 10)** – reduce repetitive usings across files.
> - **File‑scoped namespaces (C# 10)** – cleaner, less indentation.
>
> These features make code more expressive, less error‑prone, and easier to maintain.

---

### 12.2 What are records in C#, and how do they differ from classes?

> Records are reference types that are **designed for immutable data** and **value‑based equality**.
>
> Differences from normal classes:
> - Two record instances with the same property values are considered equal (`Equals`, `GetHashCode`, and deconstructors are generated).
> - They have concise syntax:
>   ```csharp
>   public record Person(string Name, int Age);
>   ```
> - They’re ideal for DTOs, messages, or domain entities where immutability and structural equality are desired.
>
> You can still have mutable properties, but the main intention is to model data, not behavior.

---

### 12.3 What are pattern matching enhancements (switch expressions, property patterns)?

> Recent C# versions enhanced pattern matching significantly:
>
> - **Switch expressions**:
>   ```csharp
>   var result = shape switch
>   {
>       Circle c    => $"Circle with radius {c.Radius}",
>       Rectangle r => $"Rectangle {r.Width}x{r.Height}",
>       _           => "Unknown shape"
>   };
>   ```
>   They’re more concise and expression‑based compared to the old `switch` statement.
>
> - **Property patterns**:
>   ```csharp
>   if (person is { Age: > 18, Name: "Alice" })
>   {
>       // Adult named Alice
>   }
>   ```
>   This lets you match based on object properties directly in the pattern.
>
> Overall, pattern matching makes code for branching and deconstruction more readable and expressive.

---

### 12.4 What are nullable reference types, and how do they change your coding style?

> Nullable reference types (NRTs) make nullability explicit in the type system:
> - `string` – non‑nullable reference type; compiler assumes it’s never null.
> - `string?` – nullable reference type; allowed to be null.
>
> When you enable NRTs:
> - The compiler warns if you:
>   - Assign `null` to a non‑nullable reference.
>   - Dereference a reference that might be null.
> - This pushes you to:
>   - Initialize properties properly.
>   - Check for null where needed.
>   - Model optional values explicitly as `?`.
>
> It improves reliability by catching potential null reference issues at compile time instead of at runtime.

---

### 12.5 What are local functions and expression‑bodied members?

> **Local functions**:
> - Functions defined inside another method.
> - Useful for encapsulating helper logic that is only relevant inside that one method, without polluting the class’s public API.
> ```csharp
> void ProcessItems(IEnumerable<int> items)
> {
>     foreach (var item in items)
>     {
>         if (IsValid(item)) { ... }
>     }
>
>     bool IsValid(int value) => value > 0;
> }
> ```
>
> **Expression‑bodied members**:
> - A concise syntax for methods, properties, constructors, etc., that have a single expression:
> ```csharp
> public int Square(int x) => x * x;
> public override string ToString() => $"{FirstName} {LastName}";
> ```
>
> They improve readability for simple members and reduce boilerplate.

---

## 13. Behavioral / Soft Skills

### 13.1 How do you keep your .NET/C# knowledge up to date?

> I try to keep up to date by:
> - Following the official **Microsoft .NET/C# blogs and docs**.
> - Reading release notes for new .NET and C# versions.
> - Watching conference talks and community content (YouTube, blogs, newsletters).
> - Experimenting with new features in small side projects.
> - Participating in code reviews and discussions with colleagues, which exposes me to different patterns and practices.

---

### 13.2 Tell me about a challenging technical problem you solved in .NET.

Use STAR, e.g.:

> We had a performance issue where a report endpoint was taking over 30 seconds to respond.
> - **Situation**: The endpoint queried multiple related tables via EF Core.
> - **Task**: I needed to reduce the response time to a few seconds.
> - **Action**:
>   - Profiled the SQL generated by EF Core using logs and SQL Server tools.
>   - Found that lazy loading was causing N+1 queries and large amounts of data were fetched unnecessarily.
>   - Refactored the query to use eager loading with specific `Include`s and `Select` projections to only retrieve needed columns.
>   - Added pagination to limit results.
> - **Result**:
>   - Response time dropped from >30 seconds to under 2 seconds.
>   - The fix also reduced database load, which improved overall system performance.
>
> This reinforced the importance of understanding how LINQ queries translate to SQL and not just relying on the ORM blindly.

---

### 13.3 How do you handle code reviews (giving and receiving feedback)?

> In code reviews:
> - **Giving feedback**:
>   - I focus on the code, not the person.
>   - I try to be specific and constructive: explain why a change is suggested (readability, performance, maintainability).
>   - I balance pointing out issues with acknowledging good patterns.
> - **Receiving feedback**:
>   - I see it as an opportunity to learn, not a personal criticism.
>   - I ask clarifying questions if I don’t understand a comment.
>   - If I disagree, I explain my reasoning respectfully and we discuss trade‑offs.
>
> Overall, I see code reviews as collaboration to improve the codebase and share knowledge.

---

### 13.4 How do you ensure code quality in a .NET project?

> To ensure code quality, I try to combine several practices:
> - Write **unit and integration tests** for critical logic.
> - Maintain **consistent coding standards** and naming conventions.
> - Use **code reviews** so multiple eyes see each change.
> - Apply **static analysis** and analyzers where appropriate (e.g., Roslyn analyzers, Sonar).
> - Refactor when needed to reduce technical debt instead of letting complexity accumulate.
> - Monitor production behavior (logs, metrics) and feed back issues into improvements.

---

### 13.5 Describe a time you had to quickly learn a new framework or library in .NET.

> In one project, we decided to adopt [e.g., “Blazor” or “Azure Functions”] to meet specific requirements.
> - **Situation**: We had limited time to deliver a feature using this new technology.
> - **Task**: I needed to get up to speed quickly and implement part of the solution.
> - **Action**:
>   - Started with the official docs and tutorials to understand the basics.
>   - Built a small spike/prototype to test the key features we needed.
>   - Reviewed sample projects and blog posts from the community.
>   - Brought back findings to the team and proposed patterns we could follow.
> - **Result**:
>   - We delivered the feature on time.
>   - The patterns we established early helped the rest of the team ramp up faster.
>
> This showed me the value of combining official documentation, community resources, and hands‑on experimentation.
