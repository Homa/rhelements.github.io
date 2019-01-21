# Add PatternFly Elements to AngularJs app

1. To start, scaffold an AngularJs app by using AngularJs app generator
called generator-gulp-angular. Visit this link to learn more about the
generator: (https://github.com/Swiip/generator-gulp-angular)

    ```bash
    npm install -g yo gulp bower
    npm install -g generator-gulp-angular
    mkdir angularjs-patternfly-element
    cd angularjs-patternfly-element
    yo gulp-angular
    gulp serve
    ```

2. Add /node_modules path to our build system:

    Open gulp/server.js and find this line:
    ```javascript
    routes = {
      '/bower_components': 'bower_components'
    };
    ```
    Changed it to:
    ```javascript
    routes = {
      '/node_modules': 'node_modules',
      '/bower_components': 'bower_components'
    };
    ```

    This allows us to reference and inject node modules in index file.

3.  Add Polyfill and ES5 adaptor

    Latest versions of most of the browsers except IE and FireFox, support custom elements. In next version of FireFox, Firefox  63, custom element support is included. If you want to support all browsers, you have to use polyfill. (https://caniuse.com/#feat=custom-elementsv1)

    Google Polymer team has developed a set of polyfills for custom elements support. If you target a specific browser, you can load the bundle that is needed by it. Please reference here to find the one that meets your needs: https://github.com/webcomponents/webcomponentsjs/tree/v1#how-to-use

    ```bash
    npm install @webcomponents/webcomponentsjs --save
    ```

    Next step is adding polyfills to public/index.html:

    ```html
    <!-- build:js(src) scripts/vendor.js -->
    <!-- bower:js -->
    <!-- run `gulp inject` to automatically populate bower script dependencies -->

    <!-- endbower -->
    <script src="../node_modules/@webcomponents/webcomponentsjs/custom-elements-es5-adapter.js"></script>
    <script src="../node_modules/@webcomponents/webcomponentsjs/webcomponents-loader.js"></script>

    <!-- endbuild -->

    <!-- build:js({.tmp/serve,.tmp/partials,src}) scripts/app.js -->
    <!-- inject:js -->
    <!-- js files will be automatically insert here -->

    <!-- endinject -->

    <!-- inject:partials -->
    <!-- angular templates will be automatically converted in js and inserted here -->
    <!-- endinject -->
    <!-- endbuild -->
    ```

4. Add theme

    PatternFly Elements uses a set of css variables to apply theme to all its web components. You can customize provided theme variables by changing css variable values. For more information visit: (https://rhelements.github.io/theme/).

    IE and FireFox don't support ShadowDOM. ShadyCSS provides a library to simulate ShadowDOM style encapsulation (reference: https://github.com/webcomponents/shadycss)

    Css variables file, polyfills and a hack for IE and FireFox support are included in cp-theme component. To install, run:

    ```bash
    npm install @patternfly/cp-theme --save
    ```

    #### Use PatternFly Elements theme

    Open src/index.html and add installed packages:

    ```html
    <!-- build:js(src) scripts/vendor.js -->
    <!-- bower:js -->
    <!-- run `gulp inject` to automatically populate bower script dependencies -->

    <!-- endbower -->
    <!-- Todo - add pfe-card npm path-->
    <script src="../bower_components/webcomponentsjs/custom-elements-es5-adapter.js"></script>
    <script src="../bower_components/webcomponentsjs/webcomponents-lite.js"></script>
    <!-- endbuild -->

    <!-- build:js({.tmp/serve,.tmp/partials,src}) scripts/app.js -->
    <!-- inject:js -->
    <!-- js files will be automatically insert here -->

    <!-- endinject -->

    <!-- inject:partials -->
    <!-- angular templates will be automatically converted in js and inserted here -->
    <!-- endinject -->
    <!-- endbuild -->
    <script src="../node_modules/@patternfly/cp-theme/cp-theme.umd.js"></script>
    ```

    If you don't support IE and FireFox, simply open index.html and add this css file to your app:
    ```html
    <link rel="stylesheet" href="/node_modules/@patternfly/cp-theme/cp-theme.css" />
    ```

    #### Add font:
    PatternFly Elements uses overpass font. You need add link to the font in to public/index.html file:

    ```
    <link rel="stylesheet" href="http://overpass-30e2.kxcdn.com/overpass.css" />
    ```

    ### Customize PatternFly Elements theme
    In order to customize the theme with your css variable values, go to this folder
    '/node_modules/@patternfly/cp-theme/' and copy cp-theme.umd (if you want to support all browsers) or cp-theme.css(if you don't need all browsers support) to your app folder and include it in your app. Now you can change the css variables as you wish.

5. Add PatternFly Elements web component:

    In this step, we install and include web component library that we want to use (pfe-card) in our app.

    Here are listed three options to include PatternFly Elements:


    ```bash
    npm install @patternfly/pfe-card --save
    ```

    Open src/index.html and add installed packages:

    ```html
    <!-- build:js(src) scripts/vendor.js -->
    <!-- bower:js -->
    <!-- run `gulp inject` to automatically populate bower script dependencies -->

    <!-- endbower -->
    <!-- Todo - add pfe-card npm path-->
    <script src="../bower_components/webcomponentsjs/custom-elements-es5-adapter.js"></script>
    <script src="../bower_components/webcomponentsjs/webcomponents-lite.js"></script>
    <!-- endbuild -->

    <!-- build:js({.tmp/serve,.tmp/partials,src}) scripts/app.js -->
    <!-- inject:js -->
    <!-- js files will be automatically insert here -->

    <!-- endinject -->

    <!-- inject:partials -->
    <!-- angular templates will be automatically converted in js and inserted here -->
    <!-- endinject -->
    <!-- endbuild -->
    <script src="../node_modules/@patternfly/cp-theme/cp-theme.umd.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.5/require.min.js"></script>
    <script>require(['../node_modules/@patternfly/pfe-card/pfe-card.umd.js'])</script>
    ```

    Note: Don't forget to add type="module" in script tag.

6. Using installed web component

    Open src/app/main/main.html Replace this block of code:

    ```html
    <div class="row">
      <div class="col-sm-6 col-md-4" ng-repeat="awesomeThing in main.awesomeThings | orderBy:'rank'">
        <div class="thumbnail">
          <img class="pull-right" ng-src="assets/images/{{ awesomeThing.logo }}" alt="{{ awesomeThing.title }}">
          <div class="caption">
            <h3>{{ awesomeThing.title }}</h3>
            <p>{{ awesomeThing.description }}</p>
            <p><a ng-href="{{awesomeThing.url}}">{{ awesomeThing.url }}</a></p>
          </div>
        </div>
      </div>
    </div>
    ```

    with this one:

    ```html
    <div class="row">
      <div class="col-sm-6 col-md-4" ng-repeat="awesomeThing in main.awesomeThings | orderBy:'rank'">
        <pfe-card theme="dark" priority="primary" color="accent" style="overflow: hidden; height: 250px;margin-bottom: 15px;">
          <h2 slot="header">{{ awesomeThing.title }}</h2>
          <p><a ng-href="{{awesomeThing.url}}">{{ awesomeThing.url }}</a></p>
        This is pfe-card with a dark theme.
          <div slot="footer">{{ awesomeThing.description }}</div>
        </pfe-card>
      </div>
    </div>
    ```

### Change theme by using inline style

  If you want to change a css variable value in theme, you can add inline style. For example if you want to change background color of a specific card to green, add style="--pfe-card--bg: green;" to pfe-card:

  ```html
  <div class="item" data-text="boop"></div>
  <pfe-card theme="dark" style="--pfe-card--bg: green;">
    <h2 slot="header">Dark Theme</h2>
  This is pfe-card with a dark theme.
    <div slot="footer">Text in footer</div>
  </pfe-card>
  ```

## Reveal page smoothly

By adding [reveal] attribute to body tag, behind the scene, PatternFly Elements waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event

1. Add [reveal] attribute to body tag:

  `<body reveal>`

2. Include related css file.
  You need to add a css file that contains the styles for smooth page opacity transition. Open public/index.html and add css file in the designated space for vendor css:

  ```html
  <!-- build:css({.tmp/serve,src}) styles/vendor.css -->
  <link media="all" rel="stylesheet" type="text/css" href="../node_modules/@patternfly/pfelement/pfelement.min.css">
  <!-- bower:css -->
  ```
