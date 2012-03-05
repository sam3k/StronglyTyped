# StronglyTyped

I’ll start by saying I love the loosely typed nature of JavaScript. When I had to work with strongly typed languages like Java, it always seemed like an unnecessary hassle. On the contrary, my boyfriend even though very proficient with HTML, CSS and SVG, comes from a strong Java background and hates loosely typed scripting languages. So, to tempt him into JS and keep him away from heavy abstractions like Objective-J, I wrote a little library that allows you to specify strongly typed properties (and since global variables are also properties of the window object, those as well) of various types (real JS types like Boolean, Number, String etc or even made up ones like Integer) and constants (final properties in Java). It uses ES5 getters and setters to do that and falls back to regular, loosely typed properties in non-supporting browsers.

Also, as a bonus, you get cross-browser Function.prototype.bind and Array.prototype.forEach and a robust type checking function: StronglyTyped.is(type, value).

## Supported types
The property types currently supported by StronglyTyped are:

* Array
* Boolean
* Date
* Function
* Integer
* Number
* RegExp
* String

null and undefined are valid in every type. NaN and Infinity values are accepted in both the Number and the Integer types.

If you want to use a type that’s not among the above but either is native to the browser (for example Element) or a global object, you can use the generic method StronglyTyped.property(type, object, property [, initialValue]):

    var o = {};
    
    StronglyTyped.property('Element', o, 'foo', document.body);
    
    console.log(o.foo); // prints a representation of the <body> element
    
    o.foo = document.head;
    console.log(o.foo); // prints a representation of the <head> element
    
    o.foo = 5; // TypeError: foo must be of type Element. 5 is not.
    
    
## Browser support

It should work on every browser that supports Object.defineProperty or __defineGetter__ and __defineSetter__. As you can see from kangax’s awesome compatibility tables for Object.defineProperty and __define(G|S)etter__, those are:

* Firefox 3.5+
* IE8 (only on DOM elements)
* IE9+
* Opera 10.5+
* Chrome 5+
* Safari 4+
* Konqueror 4.4+

However, it’s only verified to work in:

* Firefox 4 (Win and OSX)
* IE9+
* Opera 11.10 for OSX, Opera 11 for Windows
* Chrome (Win and OSX)
* Safari 5 (Win and OSX)

**This doesn’t mean it won’t work in the rest,** just that it hasn’t been tested there (yet). [You can load the unit tests, sort of...](http://leaverou.github.com/StronglyTyped/) in a browser you want to test and let me know about the results. 


## Examples

**Strongly Typed Variable**   
    
    StronglyTyped.string(this, 'myVar', 'hello'); // define myVar as a string with value 'hello'
    
    myVar = 4; // TypeError: Will throw an error   
  
  
**Strongly typed properties**   
    
    var o = {};
  
    StronglyTyped.boolean(o, 'foo', true);
    
    console.log(o.foo); // prints true
    
    o.foo = false;
    console.log(o.foo); // prints false
    
    o.foo = 'bar'; // TypeError: foo must be of type Boolean. bar is not.  
    
    
**Strongly typed properties** 
  
    StronglyTyped.constant(window, 'MAGIC_NUMBER', 3.1415926535);   
    
    
**Strongly typed DOM Element**

    var o = {};
    
    StronglyTyped.property('Element', o, 'foo', document.body);                           
    
    
## Credits
Thanks a lot to Max (@suprMax) for Windows testing! 