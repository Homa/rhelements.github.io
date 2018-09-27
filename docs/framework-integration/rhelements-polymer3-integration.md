# Add RH Elements to Polymer 3  app

1. To start, scaffold a Polymerjs 3 app:

    ```bash
    npm install -g bower
    npm install -g polymer-cli
    mkdir polymer-rhelements
    cd polymer-rhelements
    polymer init
    ```

    use arrow key select polymer-3-application, follow the steps and after install, run the app:

    ```bash
    polymer serve
    ```

    Open the app: [http://127.0.0.1:8000](http://127.0.0.1:8000)

2. Add ES5 adaptor
    We don’t need to install webcomponentsjs, polymer already included the package in index.html.


3. Add theme

    RH Elements uses a set of css variables to apply theme to all its web components. You can customize provided theme variables by changing css variable values. For more information visit: (https://rhelements.github.io/theme/).

    IE and FireFox don't support ShadowDOM. ShadyCSS provides a library to simulate ShadowDOM style encapsulation (reference: https://github.com/webcomponents/shadycss)

    Css variables file, polyfills and a hack for IE and FireFox support are included in cp-theme component. To install, run:

    ```bash
    npm install @rhelements/cp-theme --save
    ```

    #### Use RH Elements theme

    If you all browsers, open index.html and add this js file to your app::
    ```html
    <script src="/node_modules/@rhelements/cp-theme/cp-theme.umd.js" type="module"></script>
    ```

    If you don't support IE and FireFox, simply open index.html and add this css file to your app:
    ```html
    <link rel="stylesheet" href="/node_modules/@rhelements/cp-theme/cp-theme.css" />
    ```

    #### Add font:
    RH Elements uses overpass font. You need add link to the font in to index.html file:

    ```
    <link rel="stylesheet" href="http://overpass-30e2.kxcdn.com/overpass.css" />
    ```

    ### Customize RH Elements theme
    In order to customize the theme with your css variable values, go to this folder
    '/node_modules/@rhelements/cp-theme/' and copy cp-theme.umd (if you want to support all browsers) or cp-theme.css(if you don't need all browsers support) to your app folder and include it in your app. Now you can change the css variables as you wish.


3. Add RH Elements web component to your app:
    Open src/polymer-rhelements-app/polymer-rhelements-app.js and import the component:

    ```html
    import '@rhelements/rh-card/rh-card.js'
    ```
    and add:

    ```html
      <rh-card theme="dark" priority="primary" color="accent">
        <h2 slot="header">Dark Theme</h2>
      This is rh-card with a dark theme.
        <div slot="footer">Text in footer</div>
      </rh-card>
      <rh-card theme="light" priority="secondary" color="complement">
        <h2 slot="header">Light Theme</h2>
        <div slot="footer">Text in footer</div>
      </rh-card>
    ```

## Reveal page smoothly

By adding [reveal] attribute to body tag, behind the scene, RH Elements waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event

1. Add [reveal] attribute to body tag:

  `<body reveal>`

2. Include related css file.
  You need to add a css file that contains the styles for smooth page opacity transition. Open index.html and add this line on top of the file:
  ```
  <link rel="stylesheet" href="/node_modules/@rhelements/cp-theme/cp-theme.css" />
  ```
