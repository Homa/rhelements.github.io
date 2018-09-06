# Add web component to Vue app

1. To start, scaffold a Vuejs app:

    ```bash
    npm install -g
    vue create vue-web-component
    cd vue-web-component
    npm run serve
    ```

2. Install needed packages and add them to app:

    In this step, we install and include web component library that we want to use (rh-card) and polyfill libraries, if needed, in our app.

    Here are listed three options to include RHElements:

    - ES5 UMD compatible
        ```bash
        npm install @webcomponents/webcomponentsjs --save
        npm install requirejs --save
        npm install @rhelements/rh-card --save
        ```

        Open public/index.html and add installed packages:

        ```html
        <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
        <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>
        <script src="/node_modules/requirejs/require.js"></script>
        <script>require(['/src/rh-card/rh-card.umd.js'])</script>
        ```

    - ES6 compiled to ES5

        ```bash
        npm install @webcomponents/webcomponentsjs --save
        npm install @rhelements/rh-card --save
        ```

        Open public/index.html and add installed packages:

        ```html
        <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
        <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>
        <script src="/src/rh-card/rh-card.js" type="module"></script>
        ```

        Note: Don't forget to add type="module" in script tag.

    - ES6

        If you don't want to support IE11 or FireFox, you don't need to include any polyfill.

        ```bash
        npm install @rhelements/rh-card --save
        ```

        Open public/index.html and add installed packages:

        ```html
        <script src="/src/rh-card/rh-card.js" type="module"></script>
        ```

        Note: Don't forget to add type="module" in script tag.

4. Open src/components/HelloWorld.vue and add:

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

#Adding [reveal] to body tag

`<body [reveal]>`

By adding [reveal] attribute to body tag, behind the scene, RHElement waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event
