# Javascript Cheatsheet

## Variables

there is 3 ways to declare vars on javascript

### var

```javascript
// var (Global variable)
var framework = "Angular";
var framework = "React"; // dangerous!! two vars with the same name
console.log(framework); // React
```

### let

**let** fix the problem to create javascript duplicated name in the same scope

```javascript
// ES2015 let
let language = "Javascript";
let language = "Ruby"; // throws error language has already been declared in the same scope
console.log(language);
```

### const

Variables that was defined using **const** has a read only value, meaning a constant value

```javascript
const PI = 3.141593;
PI = 3.0; // throws error
console.log(PI); // 3.141593
```

When we use **const** for declare an object, this allows to modify the properties for that object.

```javascript
const jsFramework = {
    name: 'Angular';
};
jsFramework.name = 'React'; // property was updated but the reference cannot change
console.log(jsFramework.name); // 'React';
```

but the reference to the variable itself cannot be changed.

```javascript
jsFramework = {
  name: "Vue",
};
// throws error, cannot reassign object reference
```

### Variables scoe with let and const

```javascript
let movie = "Lord of the Rigns"; // this has global scope
var movie = "Batman v Superman"; // error movie already declared

function starWarsFan() {
  const movie = "Star wars";
  return movie;
}

function marvelFan() {
  movie = "The Avengers";
  return movie;
}

function blizzardFan() {
  const isFan = true;
  let phrase = "Warcraft";
  console.log("Before if: " + phrase);
  if (isFan) {
    let phrase = "initial text";
    phrase = "For the Horde!";
    console.log("Inside if: " + phrase);
  }
  phrase = "For the alliance!";
  console.log("After if: " + phrase);
}

console.log(movie);
console.log(starWarsFan());
console.log(marvelFan());
console.log(movie);
blizzardFan();
/* output */
// Lord of the Rings
// Star Wars
// The Avengers
// Theavengers
// Before if: Warcraft
// Inside if: For the Horde!
// After if: For the Alliance!
```

## Template Literals

with template literals we can create strings without the need to concatenate the values and create multiline strings, there is no needed \n anymore

```javascript
const book = {
  name: "Learning Javascript DataStructures and Algorithms",
};
console.log(`You are reading ${book.name}.,
    and this is a ew line
    and so is this.`);
```

## Arrow functions

arrow functions are a great way of simplifying the syntax of functions in ES2015, Consider the following example:

```javascript
var circleAreaES5 = function circleArea(r) {
  var PI = 3.14;
  var area = PI * r * r;
  return area;
};
console.log(circleAreaES5(2));
```

We can simplify the syntax to this:

```javascript
// arrow function large version
const circleArea = (r) => {
  const PI = 3.14;
  const area = PI * r * r;
  return area;
};
// arrow function simpler version
const circleArea = (r) => 3.14 * r * r;
// if the functions does not receive any argument we can use empty parentheses == const hello = () => console.log('Hello World');
console.log(circleArea(2));
```

## Default parameter values for functions

On ES2015 it's also possible to define default parameter values for functions.

```javascript
function sum(x = 1, y = 2, z = 3) {
  return x + y + z;
}
console.log(sum(4, 2)); // 9
```

Before ES2015 we would have to write the preceding function as in the following code:

```javascript
function sum(x, y, z) {
  if (x === undefined) x = 1;
  if (y === undefined) y = 2;
  if (z === undefined) z = 3;
  return x + y + z;
}
// or
function sum() {
  var x = arguments.length > 0 && arguments[0] !== undefined ? arguments[0] : 1;
  var y = arguments.length > 1 && arguments[1] !== undefined ? arguments[1] : 2;
  var z = arguments.length > 2 && arguments[2] !== undefined ? arguments[2] : 3;
  return x + y + z;
}
```

## Declaring the spread and rest operators

in ES5 we can turn arrays into parameters using the apply() function.
ES2015 has the spread operator (...) for this purpose.

```javascript
// spread operator
let params = [3, 4, 5];
console.log(sum(...params));
```

the same code written in ES5:

```javascript
console.log(sum.apply(undefined, params));
```

The spread operator can also be used as a rest parameter in functions to replace arguments.

```javascript
function restParameterFunction(x, y, ...a) {
  return x + y + a.length;
}
console.log(restParameterFunction(1, 2, "hello", true, 7));
```

the same code in ES5:

```javascript
function restParameterFunction(x, y) {
  var a = Array.prototype.slice.call(arguments, 2);
  return (x + y) * a.length;
}
console.log(restParameterFunction(1, 2, "hello", true, 7));
```

## Enhanced Object properties

### Array Destructuring

ES6 introduce the concept of array destructuring, which is a way of initializing variables at once.

```javascript
let [x, y] = ["a", "b"];
// the same as
let x = "a";
let y = "b";
```

Array destructuring can also be performed to swap values at once without the need to create temp variables.

```javascript
[x, y] = [y, x];
// the preceding code is the same as the following one:
var temp = x;
x = y;
y = temp;
```

This will be very useful when you learn sorting algorithms as thes swap values are very common.

### Propery shorthand

there is another way to destructuring objects.

```javascript
let [x, y] = ["a", "b"];
let obj = { x, y };

console.log(obj); // { x: 'a', y: 'b'}
```

The preceding code is the same as doing the following:

```javascript
var x = "a";
var y = "b";
var obj2 = { x: x, y: y };
console.log(obj2); // { x: 'a', y: 'b'}
```

### Shorthand method names

This allows developers to declare functions inside objects as if they were properties.

```javascript
const hello = {
  name: "abcdef",
  printHello() {
    console.log("Hello");
  },
};
console.log(hello.printHello());
```

## Object-Oriented Programming with classes

ES2015 also introduced a cleaner way of declaring classes. You learned that we can declare a class named Book in the object-oriented programming section this way:

```javascript
function Book(title, pages, isbn) {
  this.title = title;
  this.pages = pages;
  this.isbn = isbn;
}

Book.prototype.printTitle = function () {
  console.log(this.title);
};
```

With ES2015 we can simplify the syn tax and use the following code:

```javascript
class Book {
  constructor(title, pages, isbn) {
    this.title = title;
    this.pages = pages;
    this.isbn = isbn;
  }
  prinIsbn() {
    console.log(this.isbn);
  }
}
```

both have the same result

```javascript
let book = new Book("title", "pag", "isbn");
console.log(book.title);
book.title = "new title";
title;
console.log(book.title);
```

### Inheritance

With ES2015 ther eis also a simplified syntax to use inheritance between classes. Let's look at an example:

```javascript
class ITBook extends Book {
    constructor(title, pages, isbn, technology) {
        super(title, pages, isbn);
        this.technology = technology;
    }

    printTechnology() {
        console.log(this.technology);
    }
}

let jsBook = new ITBook('Learning JS Algorithms', '200', '1234567890', 'Javascript');
console.log(jsBook.title);
console.log(jsBook.printTechnology());
```

### Working with getters and setters

It's possible to create getter and setter functions for classes, although class attributes are not private as in other object-oriented languages(the encapsulation concept), it is good to follow a naming pattern.

```javascript
class Person {
    constructor(name) {
        this._name = name;
    }

    get name() {
        return this._name;
    }
    set name(value) {
        this._name = value;
    }
}

let lotrChar = new Person('Frodo');
console.log(lotrChar.name); // get
lotrChar.name = 'Gandalf'; // set
console.log(lotrChar.name);
lotrChar._name = 'Sam'; // _name is not private and we can still access it.
console.log(lotrChar.name);
```

## Exponentiation operator

```javascript
const area = 3.14 * Math.pow(r, 2);
```

ES2015+ also has some other functionalities, among them, we can <code>list iterators, type arrays, Set, Map, WeakSet, WeakMap, tail calls, for..of, Symbol, Array.prototype.includes</code>

## Modules

Node.js use by default CommonJS modules, there is also another popular javascript standard for modules wich is the Asyncrhonous Module Definition (AMD), RequireJS is the most popular AMD implementation.

```javascript
// calcArea.js
const circleArea = r => 3.14 * ( r ** 2);
const squareArea = s => s * s;

module.exports = {
  circleArea, squareArea
};

// 
const { circleArea ,squareArea } = require('./calcArea');
```

ES2015 introduced an official module feature in the javascript specification.

```javascript
// calcArea.js
const circleArea = r => 3.14 * ( r ** 2);
const squareArea = s =>  s * s;
export { circleArea, squareArea };
//
import { circleArea, squareArea } from './calcArea';
// or
import * as calcArea from './calcArea';
```

## Running ES2015 modules in the browser and with Node.js

use babel-cli
```bash
npm install -g babel-cli
```

then transpile code with babel your project with:
```bash
babel app.js --out-dir lib
```

also you can use flag --experimental-modules for node.js 8.5+

```bash
cd app
node --experimental-modules app.js
```

## Introducing Typescript

Typescript is an open source, gradually typed superset of Javascript created and maintained by Mycrosoft
It was created to allow developers to supercharge the Javascript language and to also make it easier to scale applications.

to get started with TypeScript, we need to instal it using npm:

```bash
npm install -g typescript
```

next we need to craete a file with the <code>.ts</code> extension such as **hello-world.ts**:

```typescript
let myName = 'Packt';
myName = 10;
```

we can compile it using: <code>tsc hello-world</code> on the terminal and we have on console the next error:

> *hello-world.ts(2,1): error TS2322: Type '10' is not assignable to type 'string'.*

This is because typescript check data types of variables, this allows to have a javascript code with less chances of errors or bugs.

### Type inference

Typescript allows us to assign a type to a variable, based on the value that was assigned to it.

```typescript
let age  = 20; // number
let existsFlag = true; // boolean
let language = 'Javascript'; // string
```
 if we don't type a variable then it is automatically types as **any** meaning it can receive any value as it is in Javascript

### Interfaces

In Typescript there area two concepts for interfaces. The first one is related to assigning a type to a variable. Consider the following code:

```typescript
interface Person {
  name: string;
  age: number;
}

function printName(person: Person) {
  console.log(person.name);
}
```

The first concept for the Typescript interface is that an interface is a thing. It's a description of the attributes and methods an object must have.

Now, let's try using the printName function:

```typescript
const john = { name: 'John', age: 21 };
const mary = { name: 'Mary', age: 21, phone: '123-45678' };
printName(john);
printName(mary);
```

The preceding code does not have any compilation errors. The variable **john** has a *name* and *age* as expected by the **printName** function. The variable **mary** has a *name* and *age*, but also has *phone* information.

Typescript has a concept called **Duck Typing**. If it looks like a duck, swims like a duck, and quacks like a ducks, then it must ne a duck!. In the example the variable **mary** behaves like the *Person* interface, so it must be a *Person*. This is a powerful feature of Typescript.

The second concept for the TypeScript interface is related to object-oriented programming. This is the same concept as in other object-oriented languages such as Java, C#, Ruby, and so on. An interface is a contract. In this contract we can define what behavior the classes or interfaces that will implement this contract should have.

```typescript
interface Comparable {
  compareTo(b): number;
}

class MyObject implements Comparable {
  age: number;

  compareTo(b): number {
    if(this.age === b.age) {
      return 0;
    }
    return this.age > b.age ? 1 : -1;
  }
}
```

The *Comparable* interface tells the MyObject class that it should implement a method called *compareTo* that receives an argument. Inside this method, we can code the required logic.

### Generics

Another powerful feature of Typescript that is useful to data structures and algorithms is the generic concept. Let's modify the Comparable interface so that we can define the type of the object the compareTo method should receive as an argument:

```typescript
interface Comparable<T> {
  compareTo(b: T) : number;
}
```

By passing the T type dynamically to the **Comparable** interface, between the diamond operator **<>**, we can specify the argument type of the c*ompareTo* function:

```typescript
class MyObject implements Comparable<MyObject> {
  age: number;
  
  compareTo(b: MyObject) : number {
    if(this.age === b.age) {
      return 0;
    }
    return this.age > b.age ? 1: -1;
  }
}
```

This is useful so that we can make sure we are comparing objects of the same type, and by using this functionality, we also get code completion from the editor.

### Other TypeScript functionalities

This was a very quick introduction to Typescript. The Typescript documentation is a great place for learning all the other functionalities and to dive into the details of the topics we quicklu covered in this chapter; it can be found at [https://www.typescriptlang.org/docs/home.html](https://www.typescriptlang.org/docs/home.html)

### Typescript compile-time checking in Javascript files

Some developers still prefer using plain Javascript to develop their code instead of Typescript. But it would be nice if we could use some of the type and error checking features in Javascript as well!

The good news is that Typescript has a special functionality that allows us to have this compile-time error and type checking! To use it, we need to have Typescript installed globally on our computer. In the first line of the Javascript files, we want to use type and error checking, so we simply need to add **// @ts-check**. The type checking is enabled when we add JSDoc to our code.
 
