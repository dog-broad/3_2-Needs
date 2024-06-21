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

To generate a new component, use the following command:
```bash
ng generate component component-name
```
or
```bash
ng g c component-name
```

This will create:
- A folder named after the component.
- A TypeScript file for the component logic.
- An HTML file for the template.
- A CSS file for the styles.
- A spec file for testing.
