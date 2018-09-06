# Add web component to React app

1. To start, scaffold a React app:

    ```bash
    create-react-app react-web-component
    cd react-web-component
    npm start
    ```

2. Add RHElements:

    In this step, we install and include an RHElement (i.e. rh-card) and polyfill libraries, if needed, in our app.

    - if support for IE11 or FireFox IS NOT needed, just install and include the web components that you want

    ```bash
    npm install @rhelements/rh-card --save
    ```

    ```html
    <script src="node_modules/@rhelements/rh-card/rh-card.js" type="module"></script>
    ```
    Note: Don't forget to add type="module".

    Or import the element into App.js

    ```
    import '@rhelements/rh-card/rh-card.js';
    ```

    - If you want to support the latest versions of most of the browsers, you have to use polyfills.

    ##POLYFILLS

    If you target a specific browser, you can load the bundle that is needed by it. Please reference here to find the one that meets your needs: https://github.com/webcomponents/webcomponentsjs/tree/v1#how-to-use

    We will use webcomponents-loader.js here to support all the latest browsers.

    ```bash
    # Installing the polyfill library
    npm install @webcomponents/webcomponentsjs --save
    ```

    Add pollyfills to public/index.html:

    ```html
    <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
    <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>
    ```

    Or
    ```
    import the unpkg or cdn versions of the polyfills.

    ```html
    <script src="https://unpkg.com/@webcomponents/webcomponentsjs@2.0.4/webcomponents-loader.js"></script>
    <script src="https://unpkg.com/@webcomponents/webcomponentsjs@2.0.4/custom-elements-es5-adapter.js"></script>
    ```
    ##ADD RHElement rh-card


    ```bash
    npm install @rhelements/rh-card --save
    npm install requirejs --save
    ```

    ```html
    <!-- If you use UMD version -->
    <script src="/node_modules/requirejs/require.js"></script>
    <script>require(['/node_modules/@rhelements/rh-card/rh-card.umd.js'])</script>
    <!--  Or -->
    <script src="/src/rh-card/rh-card.js" type="module"></script>
    ```


3. Open /src/App.js and add:

    ```html
    <rh-card theme="dark">
      <h2 slot="header">Dark Theme</h2>
    This is rh-card with a dark theme.
      <div slot="footer">Text in footer</div>
    </rh-card>
    <rh-card theme="light">
      <h2 slot="header">Light Theme</h2>
      <div slot="footer">Text in footer</div>
    </rh-card>
    ```
