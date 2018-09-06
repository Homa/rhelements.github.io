### Add web component to Polymer 3  app

1. To start, scaffold a Polymerjs 3 app:

    ```bash
    npm install -g bower
    npm install -g polymer-cli
    mkdir polymer-web-component
    cd polymer-web-component
    polymer init
    ```

    use arrow key select polymer-3-application and after install, run the app:

    ```bash
    polymer serve
    ```

    Open the app: [http://127.0.0.1:8000](http://127.0.0.1:8000)

2. We don’t need to install webcomponentsjs, polymer already included the package in index.html.

    Install requirejs and rh-card the web component library that we want to use:

    ```bash
    npm install @rhelements/rh-card --save
    ```

    Handle browser compatibility, the way you do it for Polymer app.

3. Open index.html. After the line that loads webcomponentsjs, add:

    ```html
    <script src="rh-card/rh-card.js" type="module"></script>

    ```

    Note: Don't forget to add type="module".

5. open polymer-web-component-app/polymer-web-component-app.js and add these lines in template:

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

#Adding [reveal] attribute to body tag

`<body [reveal]>`

By adding [reveal] attribute to body tag, behind the scene, RHElement waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event
