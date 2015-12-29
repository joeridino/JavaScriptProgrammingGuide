# JavaScript Programming Guide
*A guide for creating consistent and pretty JavaScript programs*

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
    
    // Your code goes here.
}());
```

### Tokens
User-defined tokens must be in camel case form.  The first character must be in lowercase.  Function constructors must start with an uppercase letter.

```JavaScript
var xCoordinate = 5;
```

```JavaScript
function doSomething () {
}
```

```JavaScript
function Person () {
}
```

### Variable Declarations
All variables must be declared with a single var statement at the top of functions.

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
There must be no newlines in an innermost function body.  Newlines are permitted to separate functions.

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
JavaScript classes must have a function constructor that sets their private variables to default values.  These variables must be prefixed with an underscore to denote their private status.  Public variables are not allowed unless the class has data properties only.  Private functions must also be prefixed with an underscore.

```JavaScript
// The Circle class is a data-only class.  There are no functions to manipulate the data, so the class variables don't start with an underscore.
function Circle () {
    this.centerX = 0;
    this.centerY = 0;
    this.radius = 0;
}

// The Person class has functions that act on the data, so no public variables are allowed.  All the variables must be prefixed with an underscore.
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
