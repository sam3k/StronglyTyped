# StronglyTyped

I’ll start by saying I love the loosely typed nature of JavaScript. When I had to work with strongly typed languages like Java, it always seemed like an unnecessary hassle. On the contrary, my boyfriend even though very proficient with HTML, CSS and SVG, comes from a strong Java background and hates loosely typed scripting languages. So, to tempt him into JS and keep him away from heavy abstractions like Objective-J, I wrote a little library that allows you to specify strongly typed properties (and since global variables are also properties of the window object, those as well) of various types (real JS types like Boolean, Number, String etc or even made up ones like Integer) and constants (final properties in Java). It uses ES5 getters and setters to do that and falls back to regular, loosely typed properties in non-supporting browsers.

Also, as a bonus, you get cross-browser Function.prototype.bind and Array.prototype.forEach and a robust type checking function: StronglyTyped.is(type, value).


## Examples

** Strongly Typed Variable **   
  StronglyTyped.string(this, 'myVar', 'hello'); // define myVar as a string with value 'hello'
  myVar = 4; // TypeError: Will throw an error   
  
** Strongly typed properties **   
  var o = {};

  StronglyTyped.boolean(o, 'foo', true);
  
  console.log(o.foo); // prints true
  
  o.foo = false;
  console.log(o.foo); // prints false
  
  o.foo = 'bar'; // TypeError: foo must be of type Boolean. bar is not.  
  
** Strongly typed properties ** 

  StronglyTyped.constant(window, 'MAGIC_NUMBER', 3.1415926535);                               