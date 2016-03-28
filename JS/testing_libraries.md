# Use the following guidelines for JS Libraries

## Suggested folder structure
```
// base namespace - use a common namespace for all your packages
emComponents

// package namespace (common grouping of components)
// em- followed by snake-case-name
em-ui-view
em-payments

// individual directives/components
// em- followed by snake-case-name
em-table
em-credit-card

// Folder organization

- For single component packages
-- /src
		/templates
		/css
		  index.js
		  otherFile.js
    /test
   		testName.spec.js
   /docs
   bower.json

- For multi-component packages
-- /src
   /componentName
     /test
     /docs
     /templates
     /css
     index.js
     otherFile.js
   /bower.json  
```

## Tools

| Tool | Use | Alternatives |
| ---- | --- | ------------ |
| Jasmine | A common test framework. Use this by default | Mocha, Chai |
| Karma | A test runner (not a framework). Karma has bundled test running server. You'll use a framework (eg. Jasmine), within this to run tests. ||
| Protractor | A test runner specifically for Angular. This is mainly for functional and integration testing. (eg. Test the whole app in the browser). This uses Selenium webdriver and Jasmine internally. See https://egghead.io/series/learn-protractor-testing-for-angularjs||

## Starting a New Library

You can only use NPM. But for easier client-side management, use NPM for dev-dependencies and use Bower for client-side dependencies.

Start Bower
```
bower init
```

Start NPM
```
npm init
```

Install Karma
```
sudo npm install karma jasmine-core karma-jasmine karma-chrome-launcher --save-dev
```

If this is your first time with Karma, install the CLI globally.
```
npm install -g karma-cli
```

Create Karma config
```
karma init
```

Download the required client-side dependencies
```
bower install --save angular
bower install --save-dev angular-mocks
```

Update `karma.conf.js` and add all the dependencies.
```
    // list of files / patterns to load in the browser
    files: [
      'bower_components/angular/angular.js',
      'bower_components/angular-mocks/angular-mocks.js',

      'bower_components/moment/moment.js',
      'bower_components/moment-timezone/moment-timezone.js',
      'bower_components/angular-moment/angular-moment.js',

      // source
      'src/**/*.js',
      'test/**/*.spec.js'
    ],
```

## Run Karma
```
karma start
```

## Reference
```
Karma is a great tool for unit testing, and Protractor is intended for end to end or integration testing. This means that small tests for the logic of your individual controllers, directives, and services should be run using Karma. Big tests in which you have a running instance of your entire application should be run using Protractor. Protractor is intended to run tests from a user's point of view - if your test could be written down as instructions for a human interacting with your application, it should be an end to end test written with Protractor.
```
- http://www.yearofmoo.com/2013/09/advanced-testing-and-debugging-in-angularjs.html
- https://karma-runner.github.io/latest/intro/installation.html



