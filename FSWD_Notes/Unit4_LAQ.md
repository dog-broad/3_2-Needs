# ngModel

**ngModel Example**

The `ngModel` directive in Angular is used for two-way data binding. It binds the value of an HTML element (like an input field) to a variable in the component and vice versa.

Here is a simple example:

`ngModel`  is not a part of Angular's code library, it is defined in the forms module library so you need to import the `FormsModule` library in your app.`module.ts` file. Now we can use the `ngModel` directive to implement two-way data binding.

**app.module.ts**
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

**app.component.ts**
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'ngModel Example';
  name: string = '';
}
```

**app.component.html**
```html
<div>
  <h1>{{ title }}</h1>
  <input [(ngModel)]="name" placeholder="Enter your name">
  <p>Hello, {{ name }}!</p>
</div>
```

#  Angular Framework

**Angular** is a platform and framework for building single-page client applications using HTML and TypeScript. Angular is written in TypeScript and provides a set of libraries for:
- Building scalable web applications.
- Implementing common features like routing, forms management, client-server communication, etc.
- Enhancing productivity with powerful templates, IDEs, and CLI.

**Features of Angular:**
- Component-based architecture.
- Supports multiple platforms (web, mobile, desktop).
- High performance with features like code splitting and lazy loading.
- Full-stack development capabilities with testing and animation support.

# Steps to Setup an Angular Application

**Setting up the local environment and workspace:**

1. **Install Node.js and npm:**
   - Download and install Node.js from [nodejs.org](https://nodejs.org/).
   - npm is included with Node.js.

2. **Install Angular CLI:**
   - Open a terminal and run the following command:
     ```bash
     npm install -g @angular/cli
     ```

3. **Create a new Angular project:**
   - Run the following command to create a new Angular project:
     ```bash
     ng new my-app
     ```
   - Navigate to the project directory:
     ```bash
     cd my-app
     ```

4. **Serve the application:**
   - Run the development server:
     ```bash
     ng serve --open
     ```
   - This will open your new Angular app in a browser at `http://localhost:4200`.

# Creating a Component with Angular CLI

Components refer to the reusable code that can be reused in different parts of an application. They are used to organize and structure the code in an Angular application. Components are used to organize and structure the code in an Angular application. They are the building blocks of an Angular application and can be reused in different parts of the application. 

To generate a new component, use the following command:
```bash
ng generate component component-name
```
or
```bash
ng g c component-name
```

- This command will create a new folder named `component-name` inside the `src/app` directory with the following files:
  - `component-name.component.ts`: The TypeScript file containing the component's logic.
  - `component-name.component.html`: The HTML template for the component.
  - `component-name.component.css`: The CSS file for the component's styles.
  - `component-name.component.spec.ts`: The test file for the component.

**Component Files Explanation:**
  - **component-name.component.ts:**
   ```typescript
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-component-name',
     templateUrl: './component-name.component.html',
     styleUrls: ['./component-name.component.css']
   })
   export class ComponentNameComponent {
     // Component logic goes here
   }
   ```

  - **component-name.component.html:**
   ```html
   <p>
     component-name works!
   </p>
   ```

  - **component-name.component.css:**
   ```css
   /* Styles for the component */
   ```

  - **component-name.component.spec.ts:**
   This file contains the test cases for the component.



# Routing

### Importance of Routing in Single-Page Applications (SPAs)

**Routing** is crucial in Single-Page Applications (SPAs) for several reasons:

1. **User Experience:**
   - Routing allows users to navigate between different views or components within the application without triggering a full page reload. This results in a smoother and faster user experience as only the necessary content is updated.

2. **State Preservation:**
   - It helps in maintaining the application state across different views. Users can go back and forth between views without losing the state of the application, such as form data or user settings.

3. **Deep Linking:**
   - Routing enables deep linking, allowing users to bookmark and share specific states or pages of the application. This is essential for usability and SEO, as it allows search engines to index the content effectively.

4. **Separation of Concerns:**
   - It helps in separating the concerns of different parts of the application. Each route can represent a distinct view or component, making the application structure more modular and manageable.

### Angular's Routing Module

Angular's `RouterModule` provides a robust way to handle routing in SPAs. It facilitates navigation between different views or components efficiently. Here’s how it works and how to set it up:

1. **Setting Up the Router:**
   - First, you need to import the `RouterModule` and `Routes` in your `AppModule`.

     ```typescript
     import { NgModule } from '@angular/core';
     import { BrowserModule } from '@angular/platform-browser';
     import { RouterModule, Routes } from '@angular/router';

     import { AppComponent } from './app.component';
     import { HomeComponent } from './home/home.component';
     import { AboutComponent } from './about/about.component';

     const routes: Routes = [
       { path: '', component: HomeComponent },
       { path: 'about', component: AboutComponent }
     ];

     @NgModule({
       declarations: [
         AppComponent,
         HomeComponent,
         AboutComponent
       ],
       imports: [
         BrowserModule,
         RouterModule.forRoot(routes)
       ],
       providers: [],
       bootstrap: [AppComponent]
     })
     export class AppModule { }
     ```

2. **Defining Routes:**
   - Routes are defined as an array of objects, each object representing a route with properties like `path` and `component`.

     ```typescript
     const routes: Routes = [
       { path: '', component: HomeComponent },
       { path: 'about', component: AboutComponent }
     ];
     ```

3. **Router Outlet:**
   - The `RouterOutlet` directive acts as a placeholder that Angular dynamically fills based on the current router state.

     ```html
     <!-- app.component.html -->
     <nav>
       <a routerLink="/">Home</a>
       <a routerLink="/about">About</a>
     </nav>
     <router-outlet></router-outlet>
     ```

4. **Navigating Between Routes:**
   - Use the `routerLink` directive to bind link elements to routes.

     ```html
     <a routerLink="/">Home</a>
     <a routerLink="/about">About</a>
     ```

5. **Programmatic Navigation:**
   - You can navigate programmatically using the `Router` service.

     ```typescript
     import { Component } from '@angular/core';
     import { Router } from '@angular/router';

     @Component({
       selector: 'app-some-component',
       template: `
         <button (click)="goToAbout()">Go to About</button>
       `
     })
     export class SomeComponent {
       constructor(private router: Router) {}

       goToAbout() {
         this.router.navigate(['/about']);
       }
     }
     ```



# `HttpClientModule` and `Observable` in Angular

### HttpClientModule

The `HttpClientModule` is an Angular module that allows you to make HTTP requests to remote servers and interact with RESTful services. It is part of the `@angular/common/http` package and provides a simplified and more powerful API than the deprecated `Http` module.

**Key Features:**
- Supports all HTTP methods: `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, etc.
- Provides methods for handling requests and responses.
- Supports interceptors for request and response transformation.
- Handles response types like JSON by default.

Example:

```typescript
import { HttpClient } from '@angular/common/http';

const http = new HttpClient();

http.get('https://api.example.com/data').subscribe(); // Make a GET request

http.post('https://api.example.com/data', {}).subscribe(); // Make a POST request

http.put('https://api.example.com/data', {}).subscribe(); // Make a PUT request

http.delete('https://api.example.com/data').subscribe();  // Make a DELETE request

http.patch('https://api.example.com/data', {}).subscribe(); // Make a PATCH request

```

### Observable

Observables are a part of the RxJS (Reactive Extensions for JavaScript) library and are used for asynchronous programming in Angular. Observables provide support for passing messages between parts of your application. They are a powerful way to handle asynchronous data streams.

**Key Features:**
- Can emit multiple values over time.
- Provide operators to transform, filter, and combine data streams.
- Work seamlessly with Angular’s `HttpClient` to handle HTTP responses.

**Example:**

```typescript
import { Observable } from 'rxjs';

const observable = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
  subscriber.complete();
});

observable.subscribe(value => console.log(value));
```

This example creates an Observable that emits the numbers 1, 2, and 3, and completes. The observable is then subscribed to, and the numbers are printed to the console.

**Exmaple usage with HTTP Requests:**

```typescript
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

const http = new HttpClient();

const observable = http.get('https://api.example.com/data');

observable.subscribe();
```

In this example, an HTTP GET request is made using the `HttpClient` and the response is wrapped in an Observable. The Observable is then subscribed to, triggering the request.
