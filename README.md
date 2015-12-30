# JavaScript Programming Guide
*A guide for creating consistent and pretty JavaScript programs.*

### JSLint
All JavaScript files must pass a JSLint check.  Use JSLint comments at the top of files.

```JavaScript
/*global J: false */
/*jslint browser: true, devel: true, nomen: true */
```

### General File Format
Each file must be wrapped with a self-executing anonymous function.  The first line in the function should be 'use strict';.

```JavaScript
(function () {
    'use strict';
    
    // Your code here
}());
```

### Indents
Indents are 4 space characters.

### Tokens
User-defined tokens must be in camel case form.  Namespaces and function constructors must start with an upper case letter.  All other tokens must start with a lowercase letter.

```JavaScript
var J = {};
J.GraphicsSystem = function () {
};
```

```JavaScript
function Person () {
}
```

```JavaScript
var xCoordinate = 5;
```

```JavaScript
function doSomething () {
}
```

### Acronyms
Acronyms must follow the camel case token style.

```JavaScript
// HTTP and URL become Http and Url
var myHttpUrl = 'http://www.example.com';
```

### Whitespace
Code inside parens is tight.  Comma-separated items have a single space after each comma.

```JavaScript
var s = sum(a, b, c);
```

```JavaScript
var f = function () {
};
```

```JavaScript
if (x === 5) {
    doSomethingForX();
}
```

```JavaScript
var result = callFunctionWithWordyParams(
    J.SystemLocator.getGraphicsSystem().loadSoundGroup('global', myCallback),
    variableForLine2,
    variableForLine3
);
```

### Brackets
Starting brackets don't have their own line.

```JavaScript
if (x === 5) {
    doSomethingForX();
} else if (y === 6) {
    doSomethingForY();
} else {
    doSomethingElse();
}
```

```JavaScript
var a = [
    0,
    1,
    2,
    3,
    4,
    5
];
```

### Variable Declarations
All variables must be declared with a single var statement at the top of functions.  Variables at position 2 and greater must indented 4 spaces after the var keyword on subsequent lines.

```JavaScript
function doSomething() {
    var x = 5,
        y = 6,
        z,
        foo = null,
        bar;
}
```

### Function Bodies
There must be no newlines in an innermost function body.  Newlines are permitted to separate variables and functions in an outer scope.

```JavaScript
(function () {
    'use strict';
    
    var x = 5,
        y = 6;
    
    function sum(a, b) {
        var sum = a + b;
        return sum;
    }
    
    function multiply(obj) {
        var i,
            result = 1;
        for (i in obj) {
            if (obj.hasOwnProperty(i)) {
                result *= obj[i];
            }
        }
        return result;
    }
}());
```

### "Classes"
JavaScript classes must have a function constructor that sets their variables to default values.  Public variables are not allowed unless the class has data properties only.  Private variables and functions must be prefixed with an underscore.

```JavaScript
// The Circle class is a data-only class.
// There are no functions to manipulate the data, so the class variables don't start with an underscore.
function Circle () {
    this.centerX = 0;
    this.centerY = 0;
    this.radius = 0;
}

// The Person class has functions that act on the data, so no public variables are allowed.
// All the variables must be prefixed with an underscore.
function Person () {
    this._name = null;
    this._age = null;
}

Person.prototype.setName = function (name) {
    this._name = name;
    this._storeNameInDatabase();
};

Person.prototype._storeNameInDatabase = function () {
    // Database code here
};
```

### Function Arguments
Functions may only take a maximum of 3 arguments.

```JavaScript
function sum(a, b, c) {
    return a + b + c;
}
```

### Classless Objects as Arguments
Try to avoid passing in arbitrary objects as function arguments.

Avoid this:

```JavaScript
function doAjax(params) {
    // Code here
}

var params = {
    method: 'POST',
    url: '/ajax.php',
};
doAjax(params);
```

Prefer this:

```JavaScript
function doAjax(ajaxSetup) {
    // Code here
}

function AjaxSetup () {
    this._method = null;
    this._url = null;
};

AjaxSetup.prototype.setMethod = function (method) {
    this._method = method;
};

AjaxSetup.prototype.getMethod = function () {
    return this._method;
};

AjaxSetup.prototype.setUrl = function (url) {
    this._url = url;
};

AjaxSetup.prototype.getUrl = function () {
    return this._url;
};

var ajaxSetup = new AjaxSetup();
ajaxSetup.setMethod('POST');
ajaxSetup.setUrl('/ajax.php');
doAjax(ajaxSetup);
```
### Callbacks
Callbacks have two arguments, an instance of an Error object, and a data result.  The Error object can be an Error itself or any child class of Error.  If there is no error, it must be set to null.  The result argument can be any data type.  Make sure to bind to 'this' when passing the callback from the context of a class.

```JavaScript
function myCallback(err, result) {
}
```

```JavaScript
function Person() {
}

Person.prototype.myTimeoutCallback = function (err, result) {
};

Person.prototype.doSomething = function () {
    setTimeout(this.myTimeoutCallback.bind(this), 2000);
};
```
