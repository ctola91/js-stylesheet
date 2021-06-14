# Arrays

An **array** is the simplest memory data structure. All programming languages have a built-in array datatype.

An Array stores values that are all of the same datatype sequentially. Although JavaScript allows us to create arrays with values from different datatypes, we will follow best practices and assume that we cannot do this.

## Why should we use arrays?

Let's consider that we need to store the average temperature of each month of the year for the city that we live in.

```javascript
const averageTempJan = 31.9;
const averageTempFeb = 35.3;
const averageTempMar = 42.4;
const averageTempApr = 52;
const averageTempMay = 60.8;
...
```

This is not the best approach, Here is comming arrays to help our solution.

```javascript
const averageTemp = [];
averageTemp[0] = 31.9;
averageTemp[1] = 35.3;
averageTemp[2] = 42.4;
averageTemp[3] = 52;
averageTemp[4] = 60.8;
```

## Creating and initializing arrays

Declaring, creating and initializing an array in Javascript is really simple:

```javascript
let daysOfWeek = new Array(); // using the keyword new
daysOfWeek = new Array(7); // using the keyword new with a length of the array
daysOfWeek = new Array(
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday"
); // pass the elements directly to its constructor
daysOfWeek = []; // best practice
```

However, using the new keyword is not considered best practice. if we want to create an array in Javascript we can assign empty brackets or initialize the array with some elements:

```javascript
let daysOfWeek = []; // best practice
let daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
]; // best practice with some elements

console.log(daysOfWeek.length); // how many elements are in the array
```

## Accessing elements and iterating an array

To access a specific position of the array, we can also use brackets , passing the index of the position we would like to access.

```javascript
for (let i = 0; i < dausOfWeek.length; i++) {
  console.log(daysOfWeek[i]);
}
```

antoher example could be the fibonacci sequence, The first two numbers of the Fibonacci sequence are 0 and 1, and each subsequent number is the sum of the previous two numbers:

```javascript
const fibonacci = [];
fibonacci[1] = 0;
fibonacci[2] = 1;

for (let i = 3; i < 20; i++) {
  fibonacci[i] = fibonacci[i - 1] + fibonacci[i - 2];
}
for (let i = 1; i < fibonacci.length; i++) {
  console.log(fibonacci[i]);
}
```

## Adding elements

Adding and removing elements from an array is not that difficult; however, it can be tricky, we use the next array for samples:

```javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
```

### Inserting an element at the end of the array

if we want to add a new element to this array, all we have to do is reference the latest free position of the array and assign a value to it:

```javascript
numbers[numbers.length] = 10;
```

> **Important**, in other languages like C or Java we need to determine the size of the array, so the size is static, instead of that on Javascript we can easily add new elements to it. because an array is a mutable object in javascript, the object will grow dynamically as we add new elements to it.

### Using the push method

Javascript APi also has a method called push that allows us to add new elements to the end of an array. We can add as many elements as we want as arguments to the push method:

```javascript
numbers.push(11);
numbers.push(12, 13);
```

### Inserting an element in the first position

we can move all elements to the right using a loop and insert our value to the position 0:

```javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

Array.prototype.insertFirstPosition = function (value) {
  for (let i = this.length; i >= 0; i--) {
    this[i] = this[i - 1];
  }
  this[0] = value;
};
numbers.insertFirstPosition(-1);
```

### using the unshift method

Javascript Array class also has a method called unshift, which inserts the values passed in the method's arguments at the start of the array (the logic behind-the-scenes has the same behavior as the insertFirstPosition method):

```javascript
numbers.unshift(-2);
numbers.unshift(-4, -3);
```

So, using the unshift method, we can add the value -2 and then -3, and then -4 to the beginning of the numbers array.

## Removing elements

we can learn how can we remove a value from an array.

### Removing an element from the end of the array

To remove a value from the end of an array, we can use the _pop_ method:

```javascript
numbers.pop();
```

> The **push** and **pop** methods allow an array to emaulate a basic stack data structure.

### Removing an element from the first position

To remove a value from the beginning of the array, we can use the following code:

```javascript
for (let i = 0; i < numbers.length; i++) {
  numbers[i] = numbers[i + 1];
}
```

We have only overwritten the array's original values, and we did not really remove the value (as the length of the array is still the same and we have this extra _undefined_ element).

To remove the value from the array, we can also create a removeFirstPosition method with the logic described in this topic, However, to really remove the element from the array we need to create a new array and copy all values other than undefined values from the original array to the new one and assign the new array to our array:

```javascript
Array.prototype.reIndex = function (myArray) {
  const newArray = [];
  for (let i = 0; i < myArray.length; i++) {
    if (myArray[i] !== undefined) {
      newArray.push(myArray[i]);
    }
  }
  return newArray;
};

// remove first position manually and reIndex
Array.prototype.removeFirstPosition = function () {
  for (let i = 0; i < this.length; i++) {
    this[i] = this[i + 1];
  }
  return this.reIndex(this);
};

numbers = numbers.removeFirstPosition();
```

> This code should be used only for educational purposes and should not be used in real projects.

### Using the shift method

To remove an element from the beginning of the array, we can use the shift method:

```javascript
numbers.shift();
```

> The **shift** and **unshift** methods allow an array emulate a basic queue data structure.

## Adding and removing elements from a specific position

We can use the **splice** method to remove an element from an arraay by simply specifying the position/index that we would like to delete from and how many elements we would like to remove:

```javascript
numbers.splice(5, 3);
```

This code will remove three elements, starting from index 5 of our array (<code>numbers[5]</code>, <code>numbers[6]</code>, <code>numbers[7]</code> will be removed from the <code>numbers</code> array).

> As with JavaScript arrays and objects, we can also use the **delete** operator to remove an element from the array, for example <code>delete numbers[0]</code>. However position 0 of the array will have the value **undefined**, so for this reason We should always use the <code>splice, pop or shift</code> methods to remove elements.

Now let's say we want to insert numbers 2 to 4 back into the array, starting from position 5. We can again use the splice method to do this:

```javascript
numbers.splice(5, 0, 2, 3, 4);
```

The first argument of the method is the index we want to remove elements from or insert elements into, The second argument is the number of elements we want to remove (in this case, we do not want to remove any, so will pass the value 0). And from the third argument onward we have the values we would like to insert into the array (the elements 2, 3, 4).

Finally let's execute the following code:

```javascript
numbers.splice(5, 3, 2, 3, 4);
```

In this case we removed three elements from the index 5 and we are also adding the elements 2, 3, and 4, starting at index 5.

## Two-dimensional and multi-dimensional arrays

We can use a matrix(a two-dimensial array or an _array of arrays_) to store two dimensional information:

```javascript
let averageTemp = [];
averageTemp[0] = [72, 75, 79, 79, 81, 81];
averageTemp[1] = [81, 79, 75, 75, 73, 72];
```

Javascript only support one-dimensional arrays; it does not support matrices. However, we can implement matrices or any multi-dimensional array using an array of arrays, te same can also be written as follows:

```javascript
// day 1
averageTemp[0] = [];
averageTemp[0][0] = 72;
averageTemp[0][1] = 75;
averageTemp[0][2] = 79;
averageTemp[0][3] = 79;
averageTemp[0][4] = 81;
averageTemp[0][5] = 81;
// day 2
averageTemp[1] = [];
averageTemp[1][0] = 81;
averageTemp[1][1] = 79;
averageTemp[1][2] = 75;
averageTemp[1][3] = 75;
averageTemp[1][4] = 73;
averageTemp[1][5] = 73;
```

## Iterating the elements of two-dimensional arrays

If we want to verify the output of the matrix, we can create a generic function to log its output.

```javascript
function printMatrix(myMatrix) {
  for (let i = 0; i < myMatrix.length; i++) {
    for (let j = 0; j < myMatrix[i].length; j++) {
      console.log(myMatrix[i][j]);
    }
  }
}

printMatrix(averageTemp);
```

> The output a two-dimensional array in the browser console, we can also use the `console.table(averageTemp)` statement, for a more user-friendly output.

### Multi-dimensional arrays

We can also work with multi-dimensional arrays in Javascript

```javascript
const matrix3x3x3 = [];
for (let i = 0; i < 3; i++) {
  matrix3x3x3[i] = []; // we need to initialize each array
  for (let j = 0; j < 3; j++) {
    matrix3x3x3[i][j] = [];
    for (let z = 0; z < 3; z++) {
      matrix3x3x3[i][j][z] = i + j + z;
    }
  }
}
```

If we had a 3x3x3x3 matrix we would have four nested for statements in our code and so on. You rarely will need a four-dimensional array in your career as a developer. Two dimensional arrays are most common

## References for Javascript array methods

Arrays in Javascript are modified objects, meaning that every array we create has a few methods available to be used.

Javascript arrays are very interesting because they are very powerful and have more capabilities available than primitive arrays in other languages.

| method | description |
| ------ | ----------- |
| concat | Joins multiple arrays and returns a copy of the joined arrays |
| every | Iterates every element of the array, verifying the desired condition (function) until **false** is returned |
| filter | Creates an array with each element that evaluates to true in the function provided |
| forEach | Executes a specific function on each element of the array. |
| join | Joins all the array elements into a string |
| indexOf | Searches the array for specific elements and returns its position. |
| lastIndexOf | Returns the position of the last item in the array that matches the search criterion. |
| map | Creates a new array from a function that contains the criterion/condition and returns the elements of the array that match the criterion. |
| reverse | Reverses the array so that the last item becomes the first and vice versa. |
| slice | Returns a new array from the specified **index** |
| some | Iterates every element of the array, verifying the desired conditiion (function) until **true** is returned |
| sort | Sorts the array alphabetically or by the supplied function |
| toString | Returns the array as a string |
| valueOf | Similar to the **toString** method, returns the array as a string |

Also we can use methods like ```push, pop, shift, unshift, and splice```.

## Joining multiple arrays

Consider a scenario where you have different arrays and you need to join all of them into a single array. We could iterate each array and add each element to the final array.

Fortunately Javascript already has a method that can do this for us, named the ```concat``` method, which looks as follows:

```javascript
const zero = 0;
const positiveNumbers = [1, 2, 3];
const negativeNumbers = [-3, -2, -1];
let numbers = negativeNumbers.concat(zero, positiveNumbers);
```
