# Add web Component to AngularJs app

1. To start, scaffold an angularjs app by using angularjs app generator
called generator-gulp-angular. Visit this link for more information about the
generator:

    [https://medium.com/bitmaker-software/scaffolding-a-new-angularjs-project-db01151f16e0](https://medium.com/bitmaker-software/scaffolding-a-new-angularjs-project-db01151f16e0)

    ```bash
    npm install -g yo gulp bower
    npm install -g generator-gulp-angular
    mkdir angularjs-web-component
    cd angularjs-web-component
    yo gulp-angular
    gulp serve
    ```

2. Adding the installed packages

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

3. Install needed packages:

    In this step, we install and include web component library that we want to use (rh-card) and polyfill libraries, in our app.

    Here are listed three options to include RHElements:

    - ES5 UMD compatible
        ```bash
        bower install --save webcomponents/webcomponentsjs#^1.0.0
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
        npm install @webcomponents/webcomponentsjs --save
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

#Adding [reveal] attribute to body tag

`<body [reveal]>`

By adding [reveal] attribute to body tag, behind the scene, RHElement waits for WebComponentsReady event to be fired then reveals the page. This event is fired when polyfills and user scripts have loaded and custom elements have been upgraded. This event is generally not needed; however, it may be useful in some cases like testing.

For more information visit https://github.com/webcomponents/webcomponentsjs#webcomponentsready-event
