# Simble Booking style guide for AngularJS
This is a draft document to suggest some rules that our team need to follow to write our app better and easier to maintain.
Feel free to give your own contribution.

First of all, there is a very good style guide for AngularJS project and we can reuse it. Please read it carefully first: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md

This document only adds some rules for our Simble Booking project.

### Define 1 component per file, recommended to be less than 400 lines of code.

  **Why?**: One component per file promotes easier unit testing and mocking.

  **Why?**: One component per file makes it far easier to read, maintain, and avoid collisions with teams in source control.

  **Why?**: One component per file avoids hidden bugs that often arise when combining components in a file where they may share variables, create unwanted closures, or unwanted coupling with dependencies.

```javascript
  /* avoid */
  angular
      .module('app', ['ngRoute'])
      .controller('SomeController', SomeController)
      .factory('someFactory', someFactory);

  function SomeController() { }

  function someFactory() { }
```

  The same components are now separated into their own files.

```javascript
  /* recommended */

  // app.module.js
  angular
      .module('app', ['ngRoute']);
```

```javascript
  /* recommended */

  // some.controller.js
  angular
      .module('app')
      .controller('SomeController', SomeController);

  function SomeController() { }
```

```javascript
  /* recommended */

  // some.factory.js
  angular
      .module('app')
      .factory('someFactory', someFactory);

  function someFactory() { }
```

### Use named functions instead of passing an anonymous function in as a callback.

  **Why?**: This produces more readable code, is much easier to debug, and reduces the amount of nested callback code.

```javascript
  /* avoid */
  angular
      .module('app')
      .controller('DashboardController', function() { })
      .factory('logger', function() { });
```

```javascript
  /* recommended */
  angular
      .module('app')
      .controller('DashboardController', DashboardController);

  function DashboardController() { }
```

```javascript
  // logger.js
  angular
      .module('app')
      .factory('logger', logger);

  function logger() { }
```

### Use the [`controllerAs`](http://www.johnpapa.net/do-you-like-your-angular-controllers-with-or-without-sugar/) syntax over the classic controller with $scope syntax.

  **Why?**: Controllers are constructed, "newed" up, and provide a single new instance, and the `controllerAs` syntax is closer to that of a JavaScript constructor than the `classic $scope syntax`.

  **Why?**: It promotes the use of binding to a "dotted" object in the View (e.g. `customer.name` instead of `name`), which is more contextual, easier to read, and avoids any reference issues that may occur without "dotting".

  **Why?**: Helps avoid using `$parent` calls in Views with nested controllers.

```html
  <!-- avoid -->
  <div ng-controller="CustomerController">
      {{ name }}
  </div>
```

```html
  <!-- recommended -->
  <div ng-controller="CustomerController as customer">
      {{ customer.name }}
  </div>
```

### Use a capture variable for `this` when using the `controllerAs` syntax.

  **Why?**: The `this` keyword is contextual and when used within a function inside a controller may change its context. Capturing the context of `this` avoids encountering this problem.

```javascript
  /* avoid */
  function CustomerController() {
      this.name = {};
      this.sendMessage = function() { };
  }
```

```javascript
  /* recommended */
  function CustomerController() {
      let self = this;
      self.name = {};
      self.sendMessage = sendMessage;
  }
```
### \$document, \$window, \$timeout, \$interval, \$location instead of document, window, setTimeout, setInterval, location
**Why ?**
- These services are wrapped by Angular and more easily testable, they handle Angular's digest cycle thus keeping data binding in sync.


### Move front-end app to a separated repository
There are a lot of folder from backend that front-end developers doesn't need to know, but they are still there anyway. Split front-end repository from backend will increase the productivity of front-end developer.

Why?
- Reduce backend clutter from frontend developers.


### Declare modules without a variable
Why?: With 1 component per file, there is rarely a need to introduce a variable for the module.

```
/* avoid */
let app = angular.module('app', [
    'ngAnimate',
    'ngRoute',
    'app.shared',
    'app.dashboard'
]);
```

```
/* recommended */
angular
    .module('app', [
        'ngAnimate',
        'ngRoute',
        'app.shared',
        'app.dashboard'
    ]);
```

### Coding convention must be consistent
Currently, we already have HTML and JS convention, but in many files, code doesn't follow that convention. Here is some things we need to fix:
- Indent must be 4 space
- A line is ended with a semicolon

### Filename rule
Filename must describe clearly the responsibility of that file. Here is our convention for filename:
- Controller: [name].controller.js
- Service: [name].service.js
- HTML: [name].html
- LESS: [name].less
- Factory: [name].factory.js
- Filter: [name].filter.js

We don't need to add a prefix for html and less file, because we already know the responsibility for that file. For JS files, there are many  roles for each file, so we need to add a prefix.

### Move callable member to the top
```
/** Avoid */
function MyCtrl() {
  vm.getCustomerList = function() {

  }

  vm.updateCustomerInfo = function() {

  }
}
```

```
/** Recommend */
function MyCtrl() {
  let vm = this;
  vm.getCustomerList = getCustomerList;
  vm.updateCustomerInfo = updateCustomerInfo;

  function getCustomerList() {

  }

  function updateCustomerInfo() {

  }
}
```

**Why?**
- I want to identify the callable methods at the first 10 lines, instead of reading 300 lines of code.
- Easier to reuse the existing methods and reduce chance to create new duplicated code.

### Remove $inject from our source code, use another WebPack plugin instead.
Why?
- Reduce a large amount of code that we need to write.
- Reduce the possibility of errors in production build.

Here is a plugin that we can use: https://www.npmjs.com/package/webpack-angular-injector-plugin

### Make http request from service
Instead of making http request from controller, we should only call http request from a API service
Why?
- Easier to reuse API methods
- Easier to write unit test and mock response data

### Keep API services in api folder.
**Why ?**
- API methods at one place. Easier to check or update any new API methods. I don't want to search the api service through hundred of modules.
- **Decoupling API services from other UI modules**. When you want to refactor or remove a UI module later (which is very usual for front-end). The API module keeps intact.

**Note:**
If you don't want to make a global service for API. You can create an ES6 class and import it into your controller. Example:
```javascript
// booking-api.js
export default class BookingApi {
	let self = this;
	self.getBookingList = getBookingList;

	function getBookingList(listingId) {
		let url = API_URI + '/v1.0/bookings?listing_id=' + listingId;
		return fetch(url);
	}
}

// some other controller
import BookingApi from '../api/booking-api';
export default function SomeController() {
	BookingApi.getBookingList(1);
}
```
*This is just an alternative way, AngularJS DI just works fine for me*

### Create a directive for reuse a feature easier
If we notice a features can be reused across the app, we must create a new directive to reuse it. For example, we have image-uploader to handle image crop task because we have to upload and crop image at: sidebar, listing, promote page.

### Directive Component Names

- Use consistent names for all directives using camel-case.
- Use a short prefix to describe the area that the directives belong.
```
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

## Completely remove var, only use let or const
Declare a variable by *var* can lead to many bugs because you can declare a variable twice. *let* and *const* keyword only allow you declare a variable once. Using *const* when you don't want to change the value of variable.

### Declare one variable by one line, stop a comma
```
/** Avoid */
let link = 'saas.auth',
    app = angular.module(link, [
        SignIn.name,
        SignUp.name,
        Forgot.name
    ]).config(route);
```

```
/** Recommend */
let link = 'saas.auth';
let app = angular.module(link, [
    SignIn.name,
    SignUp.name,
    Forgot.name
]).config(route);
```
**Why ?**
When you chain the variables, it’s harder to remove an unused variable, you can’t also place a Chrome breakpoint for particulate variable.


