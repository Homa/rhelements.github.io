# Add PatternFly Elements to Vue app

1. To start, scaffold a Vuejs app:

    ```bash
    npm install -g
    vue create vue-patternfly-element
    cd vue-patternfly-element
    npm run serve
    ```

2. Install needed packages and add them to app:

    In this step, we install and include web component library that we want to use (pfe-card) and polyfill libraries, if needed, in our app.

    Here are listed three options to include RH Elements:

    - ES5 UMD compatible
        ```bash
        npm install @webcomponents/webcomponentsjs --save
        npm install requirejs --save
        npm install @patternfly/pfe-card --save
        ```

        Open public/index.html and add installed packages:

        ```html
        <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
        <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>
        <script src="/node_modules/requirejs/require.js"></script>
        <script>require(['/src/pfe-card/pfe-card.umd.js'])</script>
        ```

    - ES6 compiled to ES5

        ```bash
        npm install @webcomponents/webcomponentsjs --save
        npm install @patternfly/pfe-card --save
        ```

        Open public/index.html and add installed packages:

        ```html
        <script src="/node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
        <script src="/node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>
        <script src="/src/pfe-card/pfe-card.js" type="module"></script>
        ```

        Note: Don't forget to add type="module" in script tag.

    - ES6

        If you don't want to support IE11 or FireFox, you don't need to include any polyfill.

        ```bash
        npm install @patternfly/pfe-card --save
        ```

        Open public/index.html and add installed packages:

        ```html
        <script src="/src/pfe-card/pfe-card.js" type="module"></script>
        ```

        Note: Don't forget to add type="module" in script tag.

4. Open src/components/HelloWorld.vue and add:

    ```html
    <pfe-card theme="dark">
      <h2 slot="header">Dark Theme</h2>
    This is pfe-card with a dark theme.
      <div slot="footer">Text in footer</div>
    </pfe-card>
    <pfe-card theme="light">
      <h2 slot="header">Light Theme</h2>
      <div slot="footer">Text in footer</div>
    </pfe-card>
    ```

## Reveal page smoothly

By adding [reveal] attribute to body tag, behind the scene, PatternFly Elements waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event

1. Add [reveal] attribute to body tag:

  `<body reveal>`

2. Include related css file.
  You need to add a css file that contains the styles for smooth page opacity transition. Open src/index.js and add this line on top of the file:
  ```
  import '@patternfly/pfelement/pfelement.min.css';
  ```
