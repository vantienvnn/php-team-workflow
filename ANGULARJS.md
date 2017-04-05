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
│   └── setting
│   │   ├── listings
│   │   │   └── listings.controller.js
│   │   │   └── listings.modules.js
│   │   ├── businesses
│   │   │   ├── businesses.controller.js
│   │   │   ├── businesses.module.js
│   │   │   └── businesses.scss
│   │   │   └── businesses.html
│   │   ├── ...
├── layout
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
 
## Naming conventions
The following table is shown the naming conventions for every element:

Element | Naming style | Example | usage
----|------|----|--------
Modules | lowerCamelCase  | angularApp |
Controllers | Functionality + 'Controller'  | AdminController |
Directives | lowerCamelCase  | userInfo |
Filters | lowerCamelCase | userFilter |
Services | UpperCamelCase | User | constructor
Factories | lowerCamelCase | dataFactory | others
