# Angular 6 the Complete Guide

#### First project

```shell
# creating a new project
ng new my-first-app

# compiling and serving a project
ng serve
```

##### Directories

- e2e - end 2 end testing
- node_modules - dependencies
- src - source code
  - app - our app code

#### Boostrap styling

1. Installation

   ```shell
   npm i --save bootstrap3
   ```

2. Add bootstrap in **Angular.json** file.

   ```json
   "styles": [
   	           "node_modules/bootstrap3/dist/css/bootstrap.min.css",
       	       "src/styles.css"
             ]
   ```

#### Starting application

1. Index.html is read and loaded the root component

   ```html
   <body>
     <app-root></app-root>
   </body>
   ```

2. main.ts - runs

   ```typescript
   // main.ts
   import { AppModule } from './app/app.module';
   ```

3. app.module.ts is loaded

   ```typescript
   // app.module.ts
   // AppComponent will be loaded
   bootstrap: [AppComponent]
   ```

#### Components

- .component.html - template
- .component.css - styling
- .component.ts - controler (typescript)
- .module.ts - declarations of app elements  ie. imported modules

##### .component.ts file

###### @Component section

- `selector` - name of a custom selector ie. `<my-selector>`

###### export class AppComponent{}

- variables will be available as model on the template

##### .component.html file

```html
<!-- directive, values provided  by user will be stored in a model under "name" key-->
<input type="text" [(ngModel)]="name">
<!-- output - model-->
<p>{{ name }}</p>
```

##### Creating a new component manualy

1. Everytning goes under **app** directory

2. Create a directory with a name of your new component ie. **server**

3. Inside **server** directory create

   - server.component.ts 

     ```typescript
     import { Component } from '@angular/core';

     @Component({
         selector: 'app-server',
         templateUrl: './server.component.html'
     })
     export class ServerComponent {

     }
     ```

   - server.component.html

4. Rigister your component in app.module.ts

   ```typescript
   import { ServerComponent } from './server/server.component';

   @NgModule({
     declarations: [
       AppComponent,
       ServerComponent // <--- my component
     ], //adding other Angular modules
     imports: [
       BrowserModule,
       FormsModule
     ],
     providers: [],
     bootstrap: [AppComponent]
   })
   ```

##### Creating components automaticaly

```typescript
ng g c servers
```

