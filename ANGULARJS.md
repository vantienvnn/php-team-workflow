## Table of Contents

  1. [Directory structure and naming conventions](#directory-structure-and-naming-conventions)
  1. [Angular $ Wrapper Services](#angular-$-wrapper-services)
  1. [Code Strict Mode](#code-strict-mode)
  1. [Testing](#testing)
 
## Directory structure and naming conventions

Let follow like as this example
```
.
├── app
│   ├── app.modules.js
│   ├── cores
│   │   ├── auth.service.js
│   │   ├── core.module.js
│   │   ├── calendars
│   │   │   ├── calendars.directive.js
│   │   │   ├── calendars.controller.js
│   │   │   ├── calendars.html
│   │   │   └── calendars.scss
│   │   ├── maps
│   │   │   ├── maps.directive.js
│   │   │   ├── maps.controller.js
│   ├── calendars
│   │   ├── calendars.controller.js
│   │   ├── calendars.module.js
│   │   ├── calendars.html
│   │   └── calendars.scss
│   ├── bookings
│   │   ├── bookings.controller.js
│   │   ├── bookings.service.js
│   │   └── bookings.html
│   ├── listings
│   │   ├── listings.controller.js
│   │   ├── listings.service.js
│   │   └── listings.modules.js
│   ├── businesses
│   │   ├── businesses.controller.js
│   │   ├── businesses.module.js
│   │   ├── businesses.service.js
│   │   ├── businesses.scss
│   │   ├── businesses.html
│   │   └── ...
│   ├── layouts
│   │   ├── headers.controller.js
│   │   ├── headers.html
│   │   ├── footers.controller.js
│   │   ├── footers.scss
│   │   ├── footers.html
│   │   └── ...
│   ├── main.js
└── e2e-tests

```

## Basic Coding Standard

### 1. Lines
There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters; automated style checkers MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

Blank lines MAY be added to improve readability and to indicate related blocks of code.

There MUST NOT be more than one statement per line.

### 2. Indenting

Code MUST use an indent of 4 spaces, and MUST NOT use tabs for indenting.

N.b.: Using only spaces, and not mixing spaces with tabs, helps to avoid problems with diffs, patches, history, and annotations. The use of spaces also makes it easy to insert fine-grained sub-indentation for inter-line alignment.

### 3. if, else if, else

An if structure looks like the following. Note the placement of parentheses, spaces, and braces; and that else and else if are on the same line as the closing brace from the earlier body.

```Javascript
if (expr1) {
    // if body
} else if (expr2) {
    // else if body
} else {
    // else body;
}
```

### 4. switch, case

A switch structure looks like the following. Note the placement of parentheses, spaces, and braces. The case statement MUST be indented once from switch, and the break keyword (or other terminating keyword) MUST be indented at the same level as the case body. There MUST be a comment such as // no break when fall-through is intentional in a non-empty case body.

```Javascript
switch (expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```
### 5. while, do and same same functions ...

A while statement looks like the following. Note the placement of parentheses, spaces, and braces.

```Javascript
while (expr) {
    // structure body
}
Similarly, a do while statement looks like the following. Note the placement of parentheses, spaces, and braces.
```

## Code Rules

### 1. Define 1 component per file, recommended to be less than 400 lines of code.
It mean please don't put controllers, services ... to one file
```Javascript
/* avoid */
angular
    .module('app', ['ngRoute'])
    .controller('SomeController', SomeController)
    .factory('someFactory', someFactory);

function SomeController() { }
function someFactory() { }
```
The same components are now separated into their own files.
```Javascript
/* recommended */

// -> app.module.js
angular
    .module('app', ['ngRoute']);
```
```Javascript
/* recommended */

// -> some.controller.js
angular
    .module('app')
    .controller('SomeController', SomeController);

function SomeController() { }
```
### 2. Define small functions, no more than 50 lines (less is better) for easier to maintain and debug.
### 3. Append the controller name with the suffix Controller, Service for service
### 4. Modules Naming should be begin with app. prefix, for example: app.settings.listings, app.frontdesk.calendars
### 5. Completely remove var, only use let or const
Declare a variable by var can lead to many bugs because you can declare a variable twice. let and const keyword only allow you declare a variable once. Using const when you don't want to change the value of variable.
### 6. Use consistent names for all directives using camel-case. Use a short prefix to describe the area that the directives belong (some example are company prefix or project prefix)
```Javascript
/**
 * recommended
 */

// avenger-profile.directive.js
angular
    .module
    .directive('xxAvengerProfile', xxAvengerProfile);

// usage is <xx-avenger-profile> </xx-avenger-profile>

function xxAvengerProfile() { }
```
### 7. When using a module, avoid using a variable and instead use chaining with the getter syntax.
Why?: This produces more readable code and avoids variable collisions or leaks.
```Javascript
/* avoid */
var app = angular.module('app');
app.controller('SomeController', SomeController);

function SomeController() { }
/* recommended */
angular
    .module('app')
    .controller('SomeController', SomeController);

function SomeController() { }
```
### 8. Only set once and get for all other instances.
Why?: A module should only be created once, then retrieved from that point and after.
```Javascript
/* recommended */

// to set a module
angular.module('app', []);

// to get a module
angular.module('app');
```
### 9. Use named functions instead of passing an anonymous function in as a callback.
Why?: This produces more readable code, is much easier to debug, and reduces the amount of nested callback code.
```Javascript
/* avoid */
angular
    .module('app')
    .controller('DashboardController', function() { })
    .factory('logger', function() { });
/* recommended */

// dashboard.js
angular
    .module('app')
    .controller('DashboardController', DashboardController);

function DashboardController() { }
```
### 10. Use the controllerAs syntax over the classic controller with $scope syntax.
```Html
<!-- avoid -->
<div ng-controller="CustomerController">
    {{ name }}
</div>
<!-- recommended -->
<div ng-controller="CustomerController as customer">
    {{ customer.name }}
</div>
```
### 11. Use a capture variable for this when using the controllerAs syntax. Choose a consistent variable name such as vm, which stands for ViewModel.
```Javascript
/* avoid */
function CustomerController() {
    this.name = {};
    this.sendMessage = function() { };
}
/* recommended */
function CustomerController() {
    var vm = this;
    vm.name = {};
    vm.sendMessage = function() { };
}
```
### 12. Place bindable members at the top of the controller, alphabetized, and not spread through the controller code.
```Javascript
/* avoid */
function SessionsController() {
    var vm = this;
    vm.search = function() {
      /* ... */
    };
    vm.sessions = function() {
      /* ... */
    };
    vm.title = 'Sessions';
}
```
Convert to
```Javascript
/* recommended */
function SessionsController() {
    var vm = this;
    vm.search = search;
    vm.sessions = sessions;
    vm.title = 'Sessions';
    
    function search() {
      /* ... */
    }
    function sessions() {
      /* ... */
    }
}
```
### 13. Defer logic in a controller by delegating to services and factories.
```Javascript
/* avoid */
function OrderController($http, $q, config, userInfo) {
    var vm = this;
    vm.checkCredit = checkCredit;
    vm.isCreditOk;
    vm.total = 0;

    function checkCredit() {
        var settings = {};
        return $http.get(settings)
            .then(function(data) {
               vm.isCreditOk = vm.total <= maxRemainingAmount
            })
            .catch(function(error) {
               // Interpret error
            });
    };
}
```
Convert to
```Javascript
/* recommended */
function OrderController(creditService) {
    var vm = this;
    vm.checkCredit = checkCredit;
    vm.isCreditOk;
    vm.total = 0;

    function checkCredit() {
        return creditService.isOrderTotalOk(vm.total)
          .then(function(isOk) { vm.isCreditOk = isOk; })
          .catch(showError);
    };
    function showError(){
      /* --- */
    }
}
```
### 14. When a controller must be paired with a view and either component may be re-used by other controllers or views, define controllers along with their routes.
```Javascript
 /* avoid - when using with a route and dynamic pairing is desired */

 // route-config.js
 angular
     .module('app')
     .config(config);

 function config($routeProvider) {
     $routeProvider
         .when('/avengers', {
           templateUrl: 'avengers.html'
         });
 }
 ```
 ```Html
 <!-- avengers.html -->
<div ng-controller="AvengersController as vm">
</div>
```
Convert to
```Javascript
/* recommended */

// route-config.js
angular
    .module('app')
    .config(config);

function config($routeProvider) {
    $routeProvider
        .when('/avengers', {
            templateUrl: 'avengers.html',
            controller: 'Avengers',
            controllerAs: 'vm'
        });
}
```
```Html
<!-- avengers.html -->
<div>
</div>
```
## Angular $ Wrapper Services
* Use $document and $window instead of document and window.
* Use $timeout and $interval instead of setTimeout and setInterval .
## Code Strict Mode
* To know what strict mode please read here: https://www.w3schools.com/js/js_strict.asp
* Let sure you code can run with 'use strict'; in header of javascript files
* Let sure you code can run in an Immediately Invoked Function Expression (will be wraping automatic by webpack) for example:
```Javascript
/**
 * recommended
 *
 * no globals are left behind
 */

// -> logger.js
(function() {
    'use strict';

    angular
        .module('app')
        .factory('logger', logger);

    function logger() { }
})();

// -> storage.js
(function() {
    'use strict';

    angular
        .module('app')
        .factory('storage', storage);

    function storage() { }
})();
```
## Testing

( will update in next time )
