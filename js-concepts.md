# Apendix

**JSON** Stands for JavaScript Object Notation. It is widely used as a data storage and communication format on the Web.

**Object**

**Method** Methods are simply properties that hold function values. the special variable this in its body will point to the object that it was called on.

**Prototype** A prototype is another object that is used as a fallback source of properties. When an object gets a request for a property that it does not have, its prototype will be searched for the property, then the prototype’s prototype, and so on.

**Enumerable and nonenumerable properties.** All properties that we create by simply assigning to them are enumerable. The standard properties in Object.prototype are all nonenumerable

**Create objects without prototypes**

```js
var map = Object.create(null);
map["pizza"] = 0.069;
console.log("toString" in map);
// → false
console.log("pizza" in map);
// → true
```
**Polymorphism**  Polymorphic code can work with values of different shapes, as long as they support the interface it expects.

**`let` in a for loop**  The variable will be declared not just once for the loop, but each iteration. And, it will, helpfully, be initialized at each subsequent iteration with the value from the end of the previous iteration.

**Single threaded** one command at a time, under the hood of the browser, maybe not.

**Synchronous** One at a time, and in order

*JavaScript is single threaded synchronous on its execution*

**Invocation** Running a function, in js by using parenthesis ``()``

**function invocation** Every function creates its own Execution context

**Variable environment** Where the variables live and how they relate to each other in memory.
