# Add RHElement web component to React app

1. To start, scaffold a React app:

    ```bash
    create-react-app react-web-component
    cd react-web-component
    npm start
    ```

2.  Add Polyfill and ES5 adaptor

    Latest versions of most of the browsers except IE and FireFox, support custom elements. In next version of FireFox, Firefox  63, custom element support is included. If you want to support all browsers, you have to use polyfill. (https://caniuse.com/#feat=custom-elementsv1)

    Google Polymer team has developed a set of polyfills for custom elements support.If you target a specific browser, you can load the bundle that is needed by it. Please reference here to find the one that meets your needs: https://github.com/webcomponents/webcomponentsjs/tree/v1#how-to-use

    We will use webcomponents-loader.js here to support all the latest browsers.

    In React app, if you use Babel, even if you don't need to load polyfill, you still need to load custom-elements-es5-adapter.js. (Reference: https://reactjs.org/docs/web-components.html#using-react-in-your-web-components)

    ```bash
    # Installing the polyfill library
    npm install @webcomponents/webcomponentsjs --save
    ```

    Open index.js and add these lines on top of the file:
    ```
    import '@webcomponents/webcomponentsjs/custom-elements-es5-adapter';
    import '@webcomponents/webcomponentsjs/webcomponents-loader';
    ```

    Or you can add pollyfills to public/index.html:

    ```html
    <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
    <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>
    ```

    Or use cdn versions of the polyfills.

    ```html
    <script src="https://unpkg.com/@webcomponents/webcomponentsjs@2.0.4/webcomponents-loader.js"></script>
    <script src="https://unpkg.com/@webcomponents/webcomponentsjs@2.0.4/custom-elements-es5-adapter.js"></script>
    ```

3. Add RHElement web component:

    In this step, we install and include an RHElement (i.e. rh-card) web component in our app.

    ```bash
    npm install @rhelements/rh-card --save
    ```

    Import the element into your component file. In this example, we add it to App.js

    ```
    import '@rhelements/rh-card/rh-card';
    ```

    Or you can add pollyfills to public/index.html:
    ```html
    <script src="node_modules/@rhelements/rh-card/rh-card.js" type="module"></script>
    ```
    Note: Don't forget to add type="module".


    Or use UMD version:

    ```html
    <!-- If you use UMD version -->
    <script src="/node_modules/requirejs/require.js"></script>
    <script>require(['/node_modules/@rhelements/rh-card/rh-card.umd.js'])</script>
    <!--  Or -->
    <script src="/src/rh-card/rh-card.js" type="module"></script>
    ```


4. Open /src/App.js and add:

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

## Adding [reveal] attribute to body tag

`<body [reveal]>`

By adding [reveal] attribute to body tag, behind the scene, RHElement waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event
