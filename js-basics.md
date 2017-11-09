# JavaScript Basics
I started writing these notes down as a result of reading about the [NodeJS Knowledge Challenge](https://medium.freecodecamp.org/before-you-bury-yourself-in-packages-learn-the-node-js-runtime-itself-f9031fbd8b69).
They will contain information about: functions, variables, scopes, binding, this keyword, new keyword, closures, classes, module patterns, prototypes, callbacks, and promises. Various methods that can be used on Numbers, Strings, Arrays, Sets, Objects, and Maps. Etc., etc.

## Index
* [Functions](#1)
* [Variables](#2)
* [Is JavaScript Object-Oriented?](#3)
* [Sources](#3)

## <a name="1"></a>Functions
A javascript function is a named block of code that is executed when something calls it.
```javascript
function myFunction(p1, p2) {
    return p1 * p2;
}
```
*But what is the purpose of this?*
A function will let us reuse a piece of code so that we don't have to repeat that piece of code mulitple times. Sometimes we don't even know how many times that piece of code would need to be repeated, therefore it's convenient to be able to call it whenever it's needed. We can also give the functions different values depending on the result we need or want.
### The anatomy of a function
A JavaScript function is defined by the **function** keyword, followed by a **name** and **()**. Function names can include letters, digits, underscores and dollar signs. The parentheses may include parameters separated by commas, `(parameter1, parameter2)`. The code to be executed by calling the function is placed within the block, the curly braces `{}`.

Function **parameters** are the names listed within the parentheses in the function declaration.
Function **arguments** are the real values received by the function when it's called.
```javascript
function myFunction(parameter1, parameter2) {
    return parameter1 * parameter2;
}

var argument1 = 1;
var argument2 = 2;

myFunction(argument1, argument2);
```
Inside the function, the arguments (**parameters**) behave as local variables.
### Parameters
Parameters can have pre-defined values. This is useful when a parameter has to be set but for some reason it won't always receive a value from an argument, or when you want a default option to be overrideable.
```javascript
function myFunction(a, b, c=null) {
    console.log(a, b, c);
}

myFunction(1, 2); // => 1 2 null
myFunction(1, 2, 3); // => 1 2 3
```
### Arguments
Since there are two types of variables, complex and primitive. This can have unforseen effects within a function depending on what type of argument we pass to the function.
A complex type variable is passed by **reference** to the function, rather than a copy of the variable. JavaScript sends a pointer to the variables location in memory. If a primitive type variable is passed as a **value** to the function.
*So how can this be the source of an issue?*
As JavaScript functions aren't black boxes, as we often assume, and can't only affect the enclosing scope by returning a variable. If something is passed as a reference, it will be modified even though it might not be returned by the function. A demonstration:
```javascript
var object = {
    'foo': 'bar'
}
var num = 1;

// Passed by reference
function(obj) {
    obj.foo = 'baz';
}(object);

// => Object {foo: "baz"}
console.log(object);

// Passed by value;
function(num) {
    num = 2;
}(num);

// => 1
console.log(num);
```
It is possible to call a function with more than or less than the number of arguments it expects. If a function expecting 3 arguments only receives 2, the third will be undefined. In the case of calling with too many arguments, the superfluous argument(s) will be ignored.
```javascript
// calling the function with too many arguments
function myFunction(a, b, c){
    console.log(a, b, c);
}

myFunction(1, 2, 3, 4, 5); // => 1 2 3

// calling the function with too few arguments
function myFunction(a, b, c){
    console.log(a, b, c);
}

myFunction(1, 2); // => 1 2 undefined
```
### Calling a function
There are three ways for a function to be called, invoked.
* When an event occurs, a user clicking a button for example.
* It's called from JavaScript code
* Automatically, i.e. self-invoked.
```javascript
function myFunction(parameter1, parameter2) {
    return parameter1 * parameter2;
}

myFunction(2, 6);
```
`myFunction(2, 6);` refers to the result that the function will return, in this case that would be 12. `myFunction` refers to the function definition:
```javascript
function myFunction(parameter1, parameter2) {
    return parameter1 * parameter2;
}
```
Apart from being called as described above, a function can be used just as any other variable.
```javascript
function myFunction(parameter1, parameter2) {
    return parameter1 * parameter2;
}

var text = 'The result is: ' + myFunction(3, 7);
```
### Function Types
There are two types of functions in JavaScript. **Function Declaration** and **Function Expression**.
```javascript
// Function declaration
function myFunction(parameter1, parameter2) {
    return parameter1 * parameter2;
}

// Function expression
var myFunction = function (parameter1, parameter2) {
    return parameter1 * parameter2;
}
```
They are both called in the same way, `myFunction(1, 2)`. The difference between these two types are when they are evaluated. A **Function Declaration** can be accessed by the interpreter as it's being parsed. A **Function Expression** is part of an assignment expression. Which means that JavaScript can't evaluate it until the program has completed the assignment.
*Huh?*
The **Function Declaration** is loaded before any code is executed. Meanwhile, a **Function Expression** is loaded when the interpreter reach that specific line of code. This means that if a Function Expression is being called before it's loaded, it will generate an error. But if a Function Declaration is called, it will always work since no code can be run unless all declarations are loaded.
```javascript
// Function declaration
console.log(myFunction); // Yup, this works!
function myFunction(parameter1, parameter2) {
    return parameter1 * parameter2;
}

// Function expression
console.log(myFunction); // Error! myFunction isn't loaded yet
var myFunction = function (parameter1, parameter2) {
    return parameter1 * parameter2;
}
```
### Parsing
When parsing the code, JavaScript moves all function declarations to the top of the current scope. Therefore it doesn't matter where a function declaration is located within the code.
### Return
When a **return** statement is reached the function will stop executing. The **return** will send the value back to the caller.
```javascript
var z = myFunction(2, 5);
function myFunction(p1, p2) {
    *return* p1 * p2;
}
```
Would give `z` the value of 10.
### Blocks
A JavaScript block is something as simple as statements grouped together. Blocks are contained by a `{` and a `}`.
```javascript
// Block used as a part of a function expression.
function myFunction(p1, p2) {
    return p1 * p2;
}

```
Blocks aren't limited to functions.
```javascript
// Block used as part of a conditional statement
if (isLie(cake)) {
    triumph = true;
    makeNote('huge success');
    satisfaction += 10;
}
```
### Scope
Each block gets its own scope. A demonstration:
```javascript
var x = 3;
function myFunction() {
    var x = 2 + 2;
    console.log(x); // => 4
}
console.log(x); // => 3

```
### Debugging
A **Function Expression** doesn't require a name, thus making it an **Anonymous function**. This can pose an issue when debugging as it is impossible to know what function it is that is giving you a problem.
```javascript
/*
 * Uncaught error
 *    - (anonymous function)
 *    - window.onload
 */
function(){
    throw("error");
}();

/*
 * Uncaught error
 *    - myFunction
 *    - window.onload
 */
;!function myFunction() {
    throw("error")
}();
```
### Function Objects
Functions are first-class objects and can be treated like any other object. Meaning they can be assigned to a variable, arrays or even other objects. They can also be passed as arguments to as well as being returned from other functions. We can verify that a function is an object by running the following:
```javascript
function message() {
    console.log("hello");
}
typeof message // => function
message instanceof Object; // => true
```
## <a name="2"></a>Variables
Variables can be of two types. **Complex type**, objects and arrays, and **Primitive Type**, undefined, null, boolean, string and number.

## <a name="3"></a>Is JavaScript Object-Oriented?
Yes. No. Is the short answer. The slightly longer answer is that JavaScript is Object based. It support polymorphism, encapsulation and inheritance. But by utilizing inheritance, the encapsulation would suffer. So that means JavaScript would not qualify as purely OO. A fundamental concept in JavaScript is that every element that can hold properties and methods, are objects. Primitive data types however, are not objects.
### The object
*Why objects?* To be able to reuse code more often.
An object is a collection of properties. These can consist of primitive data types, other objects or methods, (functions). A **Constructor Function** is a function that is used to create an object. There are a few built in objects like `Array`, `Image` and `Date`.
```javascript
var Image1 = new Image();
Image1.src = "myDog.gif";
```
This piece of code creates a new `Image` object, `Image1`, and assigns and sets the property `src` to it. Awesome, huh? Let's create our own object next.
```javascript
function myFunction(){
    return 5;
}

var myObject = new myFunction();
console.log(typeof myObject);  // => "object"
```
There we are, a new object. A myFunction object stored in the myObject variable. But why isn't the number 5 stored in myObject? How come that the object is stored instead when we do return a 5. This is because of the **new** keyword. It tells JavaScript to create an object follwing the blueprint of `myFunction` constructor, also called and instance. Just like the `Image` object we can assign properties to our own objects as well.
```javascript
function myFunction(){
    return 5;
}

var myObject = new myFunction();
myObject.property = 'This is a string';
console.log(myObject.property);  // => "This is a string"
```
Though, by declaring properties as in the above example, we need to declare the property for every instance of the object. Else it will be undefined.
```javascript
function myFunction(){
}

var myObject = new myFunction();
myObject.property = 'This is a string';
console.log(myObject.property);  // => "This is a string"
var myObject2 = new myFunction();
console.log(myObject2.property);  // => undefined
```
To remedy this, we can utilize the **this** keyword. Everything that is prefixed with `this.` is going to be bound to the object.
```javascript
function myFunction(){
    this.text = 'This is a string';
}

var myObject = new myFunction();
console.log(myObject.text);  // => "This is a string"
var myObject2 = new myFunction();
console.log(myObject.text);  // => "This is a string"
```
This basically means that all objects will have `text` property. Which defaults to **This is a string** for each object created, but can be set to any value without affecting the other objects created from that constructor.
We can of course define the contents of the `text` property through an `argument`. Like so:
```javascript
function myFunction(parameter){
    this.text = parameter;
}

var myObject = new myFunction('hello');
console.log(myObject.text);  // => "hello"
var myObject2 = new myFunction('good bye');
console.log(myObject.text);  // => "good bye"
```
### Object methods
Objects can also have **methods**, which is really a function that it can perform. There are multiple ways to declare a method on an object, this is one of them:
```javascript
function myFunction() {
    this.method = function(){
        console.log('hello');
    }
}
var myObject = new myFunction();
myObject.method(); // => "hello"
```
### Object categories
There are three categories to which an object can belong to. **Native**, **Host** and **user-defined**.
* Native objects are supplied by JavaScript. Examples of these are `String`, `Number`, `Array`, `Math` etc.
* Host objects are brought by the browser. Examples of these are `window`, `document` etc.
* User-defined objects are created by the programmer.

### <a name="4"></a>Sources:
https://www.w3schools.com/js/js_functions.asp
http://markdaggett.com/blog/2013/02/15/functions-explained/
https://stackoverflow.com/a/3344397/2750877
https://stackoverflow.com/questions/107464/is-javascript-object-oriented
https://www.sitepoint.com/oriented-programming-1/
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this#As_a_constructor
https://stackoverflow.com/a/504888/2750877
http://www.dofactory.com/tutorial/javascript-function-objects
