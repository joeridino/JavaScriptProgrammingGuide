# JavaScript Programming Guide
v1.0.0

*A guide for creating consistent and pretty JavaScript programs.*

### General File Format
Each file (besides a file with just a global variable) must be wrapped with a self-executing anonymous function.  The first line in the function must be 'use strict';.  Only one 'use strict'; statement must exist in a single file.

```JavaScript
(function () {
    'use strict';
    
    // Your code here
}());
```

For your project global, it can simply be defined at the global level outside of an anonymous function:

```JavaScript
var MyProjectGlobal = {};
```

### Comments
Source code must be commented using the [JSDoc](http://usejsdoc.org) syntax.  File-level comment blocks are optional and must be omitted if they provide redundant information from a class comment block.  Functions must have a comment block above them that goes into detail about what the function does and how to use it.  Comments are illegal inside inner functions, except comment blocks that describe variables.

```JavaScript
/**
 * J Game Engine.
 * @version 1.0.0
 * @namespace
 * @global
 */
 var J = {};
```

```JavaScript
(function () {
    'use strict';
   
   /**
    * A Person is the base class for all people defined in the application.
    * @class
    */
    function Person() {
        /**
         * The person's full name.
         * @type {string}
         * @default
         */
        this._name = null;
        /**
         * The person's age (years).
         * @type {number}
         * @default
         */
        this._age = 0;
    };
    
    /**
     * Gets the person's name.
     * @return {string}
     */
     Person.prototype.getName = function () {
         return this._name;
     };
     
     /**
      * Sets the person's name.
      * @param {string} name
      * @return {Person}
      */
     Person.prototype.setName = function (name) {
         this._name = name;
         return this;
     };
}());
```

### Indents
Indents are 4 space characters.

### Tokens
User-defined tokens must be in camel case form.  Namespaces and function constructors must start with an uppercase letter.  Constants are all upper case, with underscores separating words.  All other tokens must start with a lowercase letter.

```JavaScript
// Namespace
var J = {};
```

```JavaScript
// Function Constructor
J.GraphicsSystem = function () {
};
```

```JavaScript
// Function Constructor
function Person () {
}
```

```JavaScript
// Variable
var xCoordinate = 5;
```

```JavaScript
// Constant
var MY_CONSTANT = 42;
```

```JavaScript
// Regular Function
function doSomething () {
}
```

### Acronyms
Acronyms must have lowercase letters starting at the second character.

```JavaScript
// HTTP and URL become Http and Url
var myHttpUrl = 'http://www.example.com';

// Http becomes http here
var httpUrl = 'http://www.example.com';
```

### Globals
Each JavaScript project may create at most one global variable.

### Whitespace
Code inside parens is tight.  Comma-separated items have a single space after each comma.

```JavaScript
// No space allowed after the word 'sum' here
var s = sum(a, b, c);
```

```JavaScript
// A single space after the word 'function' here is required
var f = function () {
};
```

```JavaScript
if (x === 5) {
    doSomethingForX();
}
```

```JavaScript
for (i in obj) {
    if (obj.hasOwnProperty(i)) {
    }
}
```

```JavaScript
while (!done) {
}
```

```JavaScript
var result = callFunctionWithWordyParams(
    J.SystemLocator.getAudioSystem().loadSoundGroup('global', myCallback),
    variableForLine2,
    variableForLine3
);
```

### Brackets
Starting brackets don't have their own line.  Curly braces must never be omitted from control structures with a single statement.

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

```JavaScript
// Illegal
if (x)
    console.log('x is truthy');
```

### Quotes
Single quotes must be used for strings instead of double quotes.

```JavaScript
var s = 'Hello, World!';
```

```JavaScript
var s2 = 'My name is Bob O\'Ryan';
```

```JavaScript
var html = '<div id="page1">Page1 goes here</div>';
```

### Variable Declarations
All variables must be declared with a single var statement at the top of functions in alphabetical order.  Variables at position 2 and greater must indented 4 spaces after the var keyword on subsequent lines.

```JavaScript
function doSomething() {
    var bar,
        foo = null,
        x = 5,
        y = 6,
        z;
}
```

### Switch Statements
The 'case' keyword lines up vertically with the 'switch' keyword.  The code inside a case statement and the 'break' keyword line up vertically.

```JavaScript
switch (x) {
case 9:
    y = 15;
    break;
    
case 10:
    y = 25;
    break;
    
default:
    y = 99;
    break;
}
```

### Strict Equality
Always use the strict equality operators (===, !==) instead of the equality operators (==, !=).

### Ternary Operator
Use the ternary operator only to return values, not for performing operations.  Parens must wrap the ternary expression for clarity.

```JavaScript
// Legal
var x = (y === 6 ? 7 : 8);
var lastName = (firstName === 'Bob' ? 'Smith' : 'Doe');

// Illegal
(firstName === 'Bob' ? fullName.setLastName('Smith') : fullName.setLastName('Doe'));
```

### Multi-line Statements
Never put more than one statement on a single line.

```JavaScript
// Illegal
this.doSomething(); this.process();

// Illegal
var x = 5; var y = 7;
```

### Space Savers
Don't sacrifice clarity to save space.

```JavaScript
// Illegal
this.getX = function () { return this._x; };
```

### Function Bodies
There must be no newlines in an innermost function body.  Newlines are required to separate variables and functions in an outer scope.

```JavaScript
(function () {
    'use strict';
    
    var x = 5,
        y = 6;
    
    // Legal function: small, no newlines
    function sum(a, b) {
        var result = a + b;
        return result;
    }
    
    // Legal function: small, no newlines
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
    
    // Illegal function: newlines denote function "parts".
    // These parts must be split up into separate functions.
    function functionCodeSmell(b, z) {
        var name = 'Bob',
            result = false,
            x = 5;
            
        if (b) {
            result = react();
        } else {
            result = sleep();
        }
        
        if (z === 'UNKNOWN') {
            barf();
        }
        
        return result;
    }
}());
```

### Function Arguments
Functions may only take a maximum of 3 arguments.

```JavaScript
function sum(a, b, c) {
    return a + b + c;
}
```

### Class Syntax
JavaScript classes must have a function constructor that sets their variables to default values.  Public variables are not allowed unless the class has data properties only.  Private variables and functions must be prefixed with an underscore.  Child classes may access private variables and functions of their ancestors.  There is no special protected prefix.

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
    return this;
};

Person.prototype._storeNameInDatabase = function () {
    // Database code here
};
```

### Class Constructor Side Effects
Constructors must not cause side effects such as running Ajax requests, communicating with a Database, appending elements to the DOM, and the like.  Constructors are meant for initializing class properties only.

### Class Function Layout
Public functions must be at the top of the class, with private functions at the bottom.  Getters and setters are organized in pairs with the get function first followed by the set function.

```JavaScript
function Person(id) {
    this._id = id;
    this._name = null;
    this._age = null;
}

Person.prototype.getName = function () {
    return this._name;
};

Person.prototype.setName = function (name) {
    this._name = name;
    return this;
};

Person.prototype.getAge = function () {
    return this._age;
};

Person.prototype.setAge = function (age) {
    this._age = age;
    return this;
};

Person.prototype._internalFunction = function () {
};

Person.prototype._specialFunction = function () {
};
```

### Fluent Interfaces
All setter functions must return 'this'.  Other functions that don't normally have a return value can optionally return 'this', when it makes most sense.

```JavaScript
Person.prototype.setAge = function (age) {
    this._age = age;
    return this;
};

...

Person.prototype.setName = function (name) {
    this._name = name;
    return this;
}

...

var p = new Person()
    .setAge(35)
    .setName('Bob Smith');
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
    return this;
};

AjaxSetup.prototype.getMethod = function () {
    return this._method;
};

AjaxSetup.prototype.setUrl = function (url) {
    this._url = url;
    return this;
};

AjaxSetup.prototype.getUrl = function () {
    return this._url;
};

var ajaxSetup = new AjaxSetup()
    .setMethod('POST')
    .setUrl('/ajax.php');
doAjax(ajaxSetup);
```
### Callbacks
Callbacks have two arguments, an instance of an Error object, and a data result.  The Error object can be an Error itself or any child class of Error.  If there is no error, it must be set to null.  The result argument can be any data type.  Make sure to bind to 'this' when passing the callback from the context of a class.

```JavaScript
// Simple callback function
function myCallback(err, result) {
}

// Bind example
function Person() {
}

Person.prototype.myTimeoutCallback = function (err, result) {
};

Person.prototype.doSomething = function () {
    setTimeout(this.myTimeoutCallback.bind(this), 2000);
};
```
