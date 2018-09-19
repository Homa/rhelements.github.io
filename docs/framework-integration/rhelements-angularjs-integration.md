# Add web Component to AngularJs app



1. To start, scaffold an AngularJs app by using AngularJs app generator
called generator-gulp-angular. Visit this link for more information about the
generator:

    [https://github.com/Swiip/generator-gulp-angular](hhttps://github.com/Swiip/generator-gulp-angular)

    ```bash
    npm install -g yo gulp bower
    npm install -g generator-gulp-angular
    mkdir angularjs-web-component
    cd angularjs-web-component
    yo gulp-angular
    gulp serve
    ```

2.  Add Polyfill and ES5 adaptor

    Latest versions of most of the browsers except IE and FireFox, support custom elements. In next version of FireFox, Firefox  63, custom element support is included. If you want to support all browsers, you have to use polyfill. (https://caniuse.com/#feat=custom-elementsv1)

    Google Polymer team has developed a set of polyfills for custom elements support. If you target a specific browser, you can load the bundle that is needed by it. Please reference here to find the one that meets your needs: https://github.com/webcomponents/webcomponentsjs/tree/v1#how-to-use

    ```bash
    bower install --save webcomponents/webcomponentsjs#^1.0.0
    ```

    Next step is adding polyfills to public/index.html:

    ```html
    <!-- build:js(src) scripts/vendor.js -->
    <!-- bower:js -->
    <!-- run `gulp inject` to automatically populate bower script dependencies -->

    <!-- endbower -->
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
    ```

3. Add RHElement web component:

    RHElements only support npm install. We need to add /node_modules/ path to our build system.

    Open gulp/server.js and find this line:
    ```javascript
    routes = {
        '/bower_components': 'bower_components'
    };
    ```

    Changed it to:
    ```javascript
    routes = {
      '/node_modules/': 'node_modules',
      '/bower_components': 'bower_components'
    };
    ```

    This allows us to reference and inject node modules in index file.

    In this step, we install and include web component library that we want to use (rh-card) in our app.

    Here are listed three options to include RHElements:

    - ES5 UMD compatible
        ```bash
        bower install --save requirejs
        npm install @rhelements/rh-card --save
        ```

        Next step is adding installed packages to public/index.html:

        ```html
        <!-- build:js(src) scripts/vendor.js -->
        <!-- bower:js -->
        <!-- run `gulp inject` to automatically populate bower script dependencies -->

        <!-- endbower -->
        <!-- Todo - add rh-card npm path-->
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
        <script>require(['/rh-card/rh-cta.umd.js'])</script>
        ```

    - ES6 compiled to ES5

        ```bash
        npm install @rhelements/rh-card --save
        ```

        Open src/index.html and add installed packages:

        ```html
        <!-- build:js(src) scripts/vendor.js -->
        <!-- bower:js -->
        <!-- run `gulp inject` to automatically populate bower script dependencies -->

        <!-- endbower -->
        <!-- Todo - add rh-card npm path-->
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
        <script src="/rh-card/rh-card.js" type="module"></script>
        ```

        Note: Don't forget to add type="module" in script tag.

3. Using the web component

    Replace this block of code:

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
        <rh-card theme="dark" style="overflow: hidden; height: 250px;margin-bottom: 15px;">
          <h2 slot="header">{{ awesomeThing.title }}</h2>
          <div slot="footer">
            <img class="pull-right" ng-src="assets/images/{{ awesomeThing.logo }}" alt="{{ awesomeThing.title }}">
            <a ng-href="{{awesomeThing.url}}">{{ awesomeThing.url }}</a>
            <p>{{ awesomeThing.description }}</p>
          </div>
        </rh-card>
      </div>
    </div>
    ```

## Reveal page smoothly

By adding [reveal] attribute to body tag, behind the scene, RHElement waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event

1.  Adding [reveal] attribute to body tag and include related css file:

  `<body [reveal]>`

2. You need to add css file that contains the styles for smooth page opacity transition. Open src/index.js and add this line on top of the file:
  ```
  import '@rhelements/rhelement/rhelement.min.css';
  ```
