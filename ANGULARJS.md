## Table of Contents

  1. [Naming conventions](#naming-conventions)
  1. [IIFE](#iife)
 
## Directory structure and naming conventions

```
.
├── app
│   ├── app.js
│   ├── directives
│   │   ├── calendars
│   │   │   ├── calendars.directive.js
│   │   │   ├── calendars.controller.js
│   │   │   └── calendars.html
│   │   │   └── calendars.scss
│   │   ├── maps
│   │   │   ├── maps.directive.js
│   │   │   ├── maps.controller.js
│   ├── filters
│   └── services
│   │   ├── auth.service.js
│   │   ├── listing.service.js
│   │   ├── business.service.js
│   ├── frontdesk
│   │   ├── calendars
│   │   │   ├── calendars.controller.js
│   │   │   ├── calendars.module.js
│   │   │   └── calendars.html
│   │   │   └── calendars.scss
│   │   ├── bookings
│   │   │   └── bookings.controller.js
│   │   │   └── bookings.html
│   ├── setting
│   │   ├── listings
│   │   │   └── listings.controller.js
│   │   │   └── listings.modules.js
│   │   ├── businesses
│   │   │   ├── businesses.controller.js
│   │   │   ├── businesses.module.js
│   │   │   └── businesses.scss
│   │   │   └── businesses.html
│   │   ├── ...
│   ├── layout
│   │   ├── headers
│   │   │   └── headers.controller.js
│   │   │   └── headers.html
│   │   ├── footers
│   │   │   ├── footers.controller.js
│   │   │   ├── footers.scss
│   │   │   └── footers.html
│   │   ├── ...
└── e2e-tests
```
 
## Code Rules

* Define 1 component per file, recommended to be less than 400 lines of code.
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
* Define small functions, no more than 50 lines (less is better) for easier to maintain and debug.
* Let sure you code can run with 'use strict'; in header of javascript files
* Let sure you code can run in an Immediately Invoked Function Expression (will wraping automatic by webpack) for example:
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
* Modules Naming should be begin with app. prefix, for example: app.settings.listings, app.frontdesk.calendars
