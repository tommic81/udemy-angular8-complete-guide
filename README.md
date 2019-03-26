# Angular 7 the Complete Guide

#### CLI

- [Angular CLI](https://github.com/angular/angular-cli/wiki)

- **Updating npm:** Run `[sudo] npm install -g npm`  (`sudo`  is only required on Mac/ Linux)
- **Updating the CLI**

```
[sudo] npm uninstall -g angular-cli @angular/cli 

npm cache clean 

[sudo] npm install -g @angular/cli 
```



#### First project

```shell
# creating a new project
ng new my-first-app

# compiling and serving a project
ng serve
```

##### Directories and files

- package.json - dependencies

- e2e - end 2 end testing

- node_modules - installed dependencies

- src - source code

  - app - our app code

    - .html - template

    - .css - styles

    - .module.ts - importing angular modules

    - .ts - definition of a component. Converted to js.

      ```typescript
      import { Component } from '@angular/core';
      
      @Component({
        selector: 'app-root', //component's tag. It is refered by index.html.
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
      })
      export class AppComponent {
        title = 'my-first-app';
      }
      
      ```

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
  - 'foo-selector' - normal selector
  - '[foo-selector]' - attribute selector
  - '.foo-selector' - class selector
- styleUrls - urls to css files
  - alternativaly inline styles: `styles:`
- templateUrl - urls to template files
  - alternativaly inline template:  `template:` 

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

##### Databinding

- Communication between TypeScript Code and Template

- Output Data:

  - String Interpolation - `{{data}}`

  ```
  // .html
  // displays Strings or everything what can be converted to String 
  <p>{{ 'Server' }} with ID {{ serverId }} is {{ getServerStatus() }}</p>

  //.ts
  export class ServerComponent {
      serverId = 10;
      serverStatus = 'offline';

      getServerStatus() {
          return this.serverStatus;
      }
  }

  ```

  - Property Binding - `[property]="data"`

    ```
    // .html
    <button class="btn btn-primary" [disabled]="!allowNewServer">Add Server</button>

    // .ts
    allowNewServer = false;

    constructor() {
       setTimeout(() => {
          this.allowNewServer = true;
       }, 2000);
    }
    ```

    ​

- React to User Events

  - Event Binding - `(event)="expression"`

  - For events, you don't bind to **onclick** but only to **click**

  - You can `console.log()`  the element you're interested in to see which properties and events it offers

    ```
    // .html
    <button class="btn btn-primary" [disabled]="!allowNewServer"
    (click)="onCreateServer()">Add Server</button>

    // .ts
    onCreateServer() {
        this.serverCreationStatus = 'Server was created';
      }
    ```

  - Passing events with data to the typescript

    ```
    // .html
    <input type="text" class="form-control" (input)="onUpdateServerName($event)">

    // .ts
     onUpdateServerName(event: Event) {
        this.serverName = (<HTMLInputElement> event.target).value;
      }
    ```

    ​

- Combination of Both

  - Two Way Binding - `[(ngModel)]="data"`

  - FormsModule is Required 

  - You need to add `FormsModule`  to the `imports[]`  array in the AppModule

  - Then import from `@angular/forms` 

    `import { FormsModule } from '@angular/forms';` 

  ```
  // .html
  <input type="text" class="form-control" [(ngModel)]="serverName">
  <p>{{ serverName }}</p>
  ```

##### Directives

- Instructions in the DOM

- `*ngIf` - directive checks a condition (structural directive)

  ```html
  <p *ngIf="serverCreated">Server was created, server name  is {{ serverName }}</p>
  ```

- if...else

  ```html
  <!--if serverCreated is false we will jump to noServer section-->
  <p *ngIf="serverCreated; else noServer">Server was created, server name  is {{ serverName }}</p>
  <ng-template #noServer>
      <p>No server was created!</p>
  </ng-template>
  ```

- `ngStyle` - an attribute directive

  ```html
  <p [ngStyle]="{backgroundColor: getColor()}">{{ 'Server' }} with ID {{ serverId }} is {{ getServerStatus() }}</p>
  ```

- `ngClass`

  ```html
  <!--online class is applied when condition serverStatus === 'online' is meet-->
  <p [ngStyle]="{backgroundColor: getColor()}"
  [ngClass]="{online: serverStatus === 'online'}">
  {{ 'Server' }} with ID {{ serverId }} is {{ getServerStatus() }}</p>
  ```

- ngFor

  ```html
  <!-- let <VARIABLE> of <COLLECTION>-->
  
  <app-server *ngFor="let server of servers"></app-server>
  ```

  