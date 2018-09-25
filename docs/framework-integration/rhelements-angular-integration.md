# Add RH Elements to Angular app

1. To start, scaffold an angular app:

    ```bash
    npm install -g
    ng new angular-web-component
    cd angular-web-component
    ng serve --open
    ```

2. Add required packages:

    In this step, we install and include web component library that we want to use (rh-card) and polyfill libraries, if needed, in our app.

    Here are listed three options to include RH Elements:

    - ES5 UMD compatible

      ```bash
      npm install @webcomponents/webcomponentsjs --save
      npm install requirejs --save
      npm install @rhelements/rh-card --save
      ```

      Open src/index.html and add installed packages:

      ```html
      <!-- web components es5 support -->
      <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>

      <!-- web components polyfill -->
      <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>

      <!-- load require and require RH Elements -->
      <script src="/node_modules/requirejs/require.js"></script>
      <script>require(['/src/rh-card/rh-card.umd.js'])</script>
      ```

    - ES6 compiled to ES5

      ```bash
      npm install @webcomponents/webcomponentsjs --save
      npm install @rhelements/rh-card --save
      ```

      Open src/index.html and add installed packages:

      ```html
      <!-- web components es5 support -->
      <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>

      <!-- web components polyfill -->
      <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>

      <!-- load RH Elements -->
      <script src="/src/rh-card/rh-card.js" type="module"></script>
      ```

      Note: Don't forget to add type="module" in script tag.

    - ES6

      If you don't want to support IE11 or FireFox, you don't need to include any polyfill.

      ```bash
      npm install @rhelements/rh-card --save
      ```

      Open src/index.html and add installed packages:

      ```html
      <!-- load RH Elements -->
      <script src="/src/rh-card/rh-card.js" type="module"></script>
      ```

      Note: Don't forget to add type="module" in script tag.

3. Import **CUSTOM_ELEMENTS_SCHEMA** to app module and add it to @NgModule options.
    Open `src/app/app.module.ts`.

    3.1 Import CUSTOM_ELEMENTS_SCHEMA from '@angular/core':

      ```javascript
      import { NgModule, CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';
      ```

    3.2 Add schemas to @NgModule options:

      ```javascript
      schemas: [CUSTOM_ELEMENTS_SCHEMA]
      ```

    app.module.ts should look like this:

    ```javascript
    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule, CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';
    import { AppComponent } from './app.component';
    @NgModule({
      declarations: [
        AppComponent
      ],
      imports: [
        BrowserModule
      ],
      providers: [],
      bootstrap: [AppComponent],
      schemas: [CUSTOM_ELEMENTS_SCHEMA]
    })
    export class AppModule { }
    ```

5. The app is ready to use the included web component. Simply, replace the
content of src/app/app.component.html with:

    ```html
    <rh-card theme=”dark”>
      <h2 slot=”header”>Dark Theme</h2>
      This is rh-card with a dark theme.
      <div slot=”footer”>Text in footer</div>
    </rh-card>

    <rh-card theme=”light”>
      <h2 slot=”header”>Light Theme</h2>
      <div slot=”footer”>Text in footer</div>
    </rh-card>
    ```

## Reveal page smoothly

By adding [reveal] attribute to body tag, behind the scene, RH Elements waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event

1. Add [reveal] attribute to body tag:

  `<body [reveal]>`

2. Include related css file.
  You need to add a css file that contains the styles for smooth page opacity transition. Open src/index.js and add this line on top of the file:
  ```
  import '@rhelements/rhelement/rhelement.min.css';
  ```
