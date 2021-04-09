# Javascript Cheatsheet

## Variables

there is 3 ways to declare vars on javascript

### var 
```javascript
// var (Global variable)
var framework = 'Angular';
var framework = 'React'; // dangerous!! two vars with the same name
console.log(framework); // React
```

### let

**let** fix the problem to create javascript duplicated name in the same scope

```javascript
// ES2015 let
let language = 'Javascript';
let language = 'Ruby'; // throws error language has already been declared in the same scope
console.log(language);
```

### const

Variables that was defined using **const** has a read only value, meaning a constant value

```javascript
const PI = 3.141593;
PI = 3.0; // throws error
console.log(PI) // 3.141593
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
name: 'Vue'
}
// throws error, cannot reassign object reference
```

### Variables scoe with let and const
```javascript
let movie = 'Lord of the Rigns'; // this has global scope
var movie = 'Batman v Superman'; // error movie already declared

function starWarsFan() {
    const movie = 'Star wars';
    return movie;
}

function marvelFan() {
    movie = 'The Avengers';
    return movie;
}

function blizzardFan() {
    const isFan = true;
    let phrase = 'Warcraft';
    console.log('Before if: ' + phrase);
    if(isFan) {
        let phrase = 'initial text';
        phrase = 'For the Horde!';
        console.log('Inside if: ' + phrase);
    }
    phrase = 'For the alliance!';
    console.log('After if: ' + phrase);
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
    name: 'Learning Javascript DataStructures and Algorithms'
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
}
console.log(circleAreaES5(2));
```

We can simplify the syntax to this:
```javascript
// arrow function large version
const circleArea = (r) => {
    const PI = 3.14;
    const area = PI * r * r;
    return area;
}
// arrow function simpler version
const circleArea = r => 3.14 * r * r;
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
    if(x === undefined) x = 1;
    if(y === undefined) y = 2;
    if(z === undefined) z = 3;
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


