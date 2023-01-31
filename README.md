# ES6 - ECMAScript

## FCC - ES6 module learning journal

This is the first time going through the ES6 module. There will be concepts and areas that I will not fully understand during the first cycle.
I will have to cycle through this module a few more times and add to the notes as I get more acquainted with ES6.

### Variable scope

```JS
function checkScope() {
    let i = 'function scope';
    if (true) {
        let i = 'block scope';
        console.log('block scope i is: ', i);
    }
    console.log('function scope i is: ', i);
    return i;
}
```

- the 'i' variable defined inside the if statement is separate from the one defined within the function scope.
- ```let i = 'block scope';``` applies only within the if statement block, hence the term 'block scope'.
- ```let i = 'function scope';``` applies within the entire function, with the exception of the if statement block, where the 'i' variable is declared separately, hence the term 'function scope'.

### Mutate an array declared with const

- Edit the array [5, 7, 2] to [2, 5, 7]
- There are various ways to achieve this. You could manually assign new values to each element of the array by indexing the array. I think this is the intended method for this exercise.

```JS
const s = [5, 7, 2];
function editInPlace() {
    s[0] = 2;
    s[1] = 5;
    s[2] = 7;
}
editInPlace();
```

- Secondly, you can use .pop() and .unshift() method to manipulate the array.

```JS
const s = [5, 7, 2];
function editInPlace() {
    s.pop();
    s.unshift(2);
}
editInPlace();
```

- s.pop() will remove the last element of the array.
- s.unshift(2) will enter the value '2' to the first element of the array (index[0]).
- There may be other methods to achieve this, but these are the only two that I know.

#### Object Freeze

- Prevent object data mutation by applying ```Object.freeze('object_name');```

```JS
const MATH_CONSTANTS = {
    PI: 3.14
};
Object.freeze(MATH_CONSTANTS);
```

### Arrow function

- Use arrow (=>) function to simplify multi-line functions to a single in-line function. This is useful when passing a function as an argument to another function.

```JS
const myFunc = function() {
    const myVar = "value";
    return myVar;
}
```

- The above code can be simplified by replacing the 'function' text to an arrow (=>) behind the brackets, as shown below.

```JS
const myFunc = () => {
    const myVar = "value";
    return myVar;
}
```

- If the code does not have a function body and only a return value, such as above, it can be even further simplified by removing the 'return' keyword, as well as the curly braces surrounding the code.

```JS
const myFunc = () => "value";
```

### Arrow function with parameters

```JS
var myConcat = function(arr1, arr2) {
  return arr1.concat(arr2);
};
```

- The above code (written using ES5 syntax) can be re-written using arrow functions.

```JS
const myConcat = (arr1, arr2) => arr1.concat(arr2);
```

- It takes an argument on the left side of the function (=>) and return an expression on the right side of the arrow function.
- you can even remove the brackets for the parameters if it's a single parameter function.
- NOTE: ```arr1.concat(arr2)``` can also be achieved by ```[...arr1, ...arr2]```, which is called the spread operator (covered later in the module).

### Default parameters

- You can set default parameters for function in cases where the parameters are not specified.

```JS
const greeting = (name = "Anonymous") => "Hello " + name;
```

- ```console.log(greeting("Josh"));``` will display "Hello Josh", whereas ```console.log(greeting())``` will display "Hello Anonymous".
- You can set as many default values for as many parameters as needed.

### Rest Parameters (requires further understanding)

- Rest parameters allow you to create functions that take a variable number of arguments, which are stored in an array that can be recalled from the function later.
- Rest parameters are used in function definitions, for example ```function sum(...args) {}``` to represent an indefinite number of arguments as an array.

```JS
const sum = (x, y, z) => {
    const args = [x, y, z];
    return args.reduce((a, b) => a + b, 0);
}
```

- Using rest parameters, the above code can be written as shown below.

```JS
const sum (...args) => {
      return args.reduce((a, b) => a + b, 0);
}
```

### Spread Operator

- The spread operator uses the same syntax as the rest parameter ```(...)``` but in a different manner.
- The rest parameter is used in function definitions, whereas the spread operator is used to spread, or unpack, the elements of an iterable array or string into a new array or a new string. It can also be used to spread the properties of an object.
- It can be used in array literals, function calls, or object literals.

```JS
const arr1 = [1, 2, 3, 4, 5];
let arr2;

arr2 = [...arr1] // This is the spread operator
```

- ```arr2 = [...arr1]``` will 'unpack' the elements of arr1 and insert it into arr2. ```console.log(arr2);``` will display the exact same array as arr1.

### Destructuring assignment to extract values from objects

- Destructuring assignment is newly introduced in ES6 for purposes of simplicity and efficiency when assigning values taken directly from an object.

```js
const HIGH_TEMPERATURES = {
    yesterday: 75,
    today: 77, 
    tomorrow: 80
};

const today = HIGH_TEMPERATURES.today;
const tomorrow = HIGH_TEMPERATURES.tomorrow;
```

- While leaving the object as it is, the variable assignment can be simplified, as shown below.

```js
const { today, tomorrow } = HIGH_TEMPERATURES;
```

- ```console.log(today);``` will display '77', and ```console.log(tomorrow);``` will display '80'.
- In both cases ```console.log(yesterday);``` will throw an error since it is not defined.

### Use Destructuring assignment to assign variables from objects

- Method similar to extracting values using destructuring assignment is used.

```js
const HIGH_TEMPERATURES = {
    yesterday: 75,
    today: 77, 
    tomorrow: 80
};

const highToday = HIGH_TEMPERATURE.today;
const highTomorrow = HIGH_TEMPERATURE.tomorrow;
```

- while leaving the HIGH_TEMPERATURE object as is, you can assign new variables in a simpler manner, as shown below.

```js
const {today: highToday, tomorrow: highTomorrow } = HIGH_TEMPERATURES;
```

- The above code will update the object with the new variable names.
- ```console.log(today);``` or ```console.log(tomorrow);``` will throw an error since the variable names have been newly defined.

### Destructure values from nested objects

- use the same principles used in the two previous exercises to destructure values from nested objects.

```js
const LOCAL_FORECAST = {
    yesterday: {low: 61, high: 75},
    today: {low:64, high: 77},
    tomorrow: {low:68, high: 80}
};

const lowToday = LOCAL_FORECAST.today.low;
const highToday = LOCAL_FORECAST.today.high;
```

- The above two variable assignments can be replaced using destructuring assignments, as shown below.

```js
const {today: {low: lowToday, high: highToday}} = LOCAL_FORECAST;
```

- Anything other than 'lowToday' or 'highToday' for ```console.log();``` will throw an error since they are not defined.
- Assign alternate variables for 'yesterday' and 'tomorrow' in the same manner to avoid errors.

### Use destructuring assignment to assign variables from Arrays

See the example below.

```js
const [a, b] = [1, 2, 3, 4, 5];
console.log(a, b);
```

- The above code will display the values of a and b as 1 and 2. ```console.log(a, b, c, d, e);``` will display '1, 2, 3, 4, 5'.

See the next example to see how destructuring assignment allows you to pick and choose which elements to assign to which variables.

```js
const [a, b,,, c] = [1, 2, 3, 4, 5];
console.log(a, b,,, c);
```

- In the code above, commas are used to access a desired value at any index. ```console.log(a, b,,, c);``` will display '1, 2, 5'.

I had a bit of trouble understanding the logic of the following exercise.

- Use destructuring assignment to swap the values of a and b so that the value of a becomes the value of b, and vise versa.
  
```js
let a = 8, b = 6;
```

I initially made the mistake of attempting to re-declare the variables.

```js
const [a, b] = [6, 8]; // This is incorrect. It will throw an error saying that identifiers are already declared.
```

The correct solution is shown below.

```js
[a, b] = [b, a];
```

- I didn't quite understand this at first because both sides are using the same characters.
- Since the values of a and b have already been declared (let a=8, b=6), we can assume that the above code actually looks like this.

```js
[8, 6] = [b, a];
```

- Which is essentially reassigning the declared values of a and b on the left to the variables on the right, in sequential order.
- I don't know if this logic is fully correct. But this is how I understand it at this point.

### Destructuring via rest elements

- With regards to array destructuring, there may be cases where it is necessary to collect the remainder of the elements into a separate array.

A simple example is shown below

```js
const [a, b, ...arr] = [1, 2, 3, 4, 5];
console.log(a, b);
console.log(arr);
```

- ```console.log(a, b);``` will display 1, 2. Whereas ```console.log(arr);``` will display the remaining elements in a separate array ```[3, 4, 5]```.
- It is important to note that the rest syntax (...) can be only used as the last variable in a list.
- In other words, it cannot be used to catch a sub-array in the middle of an array.

```js
[a, b, ...arr, c, d] // This cannot be executed.
```

Let's take a look at a slightly more complex exercise.

- Use a destructuring assignment with the rest syntax to remove the first two elements of an array.
- 'removeFirstTwo()' should return a sub-array with the first two elements of the original array omitted.

```js
function removeFirstTwo(list) {
    const shorterList = list; // Change this line
    return shorterList;
}

const source = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const sourceWithoutFirstTwo = removeFirstTwo(source);
```

- Assign random variables to the first two elements of the source array (list), and use a rest syntax for 'shorterList'.

```js
const [a, b, ...shorterList] = list;
```

Add it together.

```js
function removeFirstTwo(list) {
    const [a, b, ...shorterList] = list;
    return shorterList;
}

const source = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const sourceWithoutFirstTwo = removeFirstTwo(source);

console.log(source); // will display [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(removeFirstTwo(source)); // will display [ 3, 4, 5, 6, 7, 8, 9, 10 ]
```

- NOTE: If you wish to see the elements that are removed, ```console.log(a, b);``` should be entered just before ```return shorterList```.
  If you attempt to log 'a' and 'b' outside of the function (outside of the curly braces of the function), it will throw an error since 'a' and 'b' are not declared in the global scope (it's within the function scope).

Therefore,

```js
function removeFirstTwo(list) {
    const [a, b, ...shorterList] = list;
    console.log(a, b);
    return shorterList;
}

const source = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const sourceWithoutFirstTwo = removeFirstTwo(source);

console.log(source);
console.log(removeFirstTwo(source));
```

The above will display

```js
/* 
1 2
[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
1 2
[ 3, 4, 5, 6, 7, 8, 9, 10 ]
*/
```

- 1 2 are repeated since the function executes for each console.log.

### Use destructuring assignment to pass an object as a function's parameters (requires further understanding)

Use destructuring assignment within the argument to the function half to send only max and min inside the function.

```js
const stats = {
  max: 56.78,
  standard_deviation: 4.34,
  median: 34.54,
  mode: 23.87,
  min: -0.75,
  average: 35.85
};

// Only change code below this line
const half = (stats) => (stats.max + stats.min) / 2.0; 
// Only change code above this line
```

The solution to the above exercise using ES5 syntax is shown below.

```js
const half = function(stats) {
    return (stats.max + stats.min) / 2.0;
}
```

- ```console.log(half(stats))``` will execute the function(stats) and return the sum of the values of max and min in the stats object divided by 2, which is ```half = 28.015```.
- Since I've been going through the basic JS module up until now, this makes more 'visual' sense to me.
- The above exercise requires the use of destructuring.

```js
const half = ({max, min}) => (max + min) / 2.0;
```

- The above code returns the exact same result as the solution using ES5 syntax when ```console.log(half(stats))``` is called.
- The syntax ```({max, min})``` is a shorthand for destructuring the object (stats) passed as an argument into the function, and extracting the 'max' and 'min' properties of the stats object.
- The left side of the arrow function (=>) is the argument, and the right side of the arrow function is the return expression.
- On the right side of the arrow function indicates what to return when ```console.log(half(stats))``` is called.
- When called, the function will destructure the object (stats) and extract its 'max' and 'min' properties. (Left side)
- Then it will return the sum of the values of the 'max' and 'min' properties and divide it by 2 to get the average. (Right side)
- ```console.log(half(stats))``` will display 28.015.

### Create strings using template literals (requires further understanding)

INSTRUCTIONS

- Use template literal syntax with backticks to create an array of list element (li) strings.
- Each list element's text should be one of the array elements from the failure property on the result object and have a class attribute with the value text-warning.
- The makeList function should return the array of list item strings.

```js
const result = {
  success: ["max-length", "no-amd", "prefer-arrow-functions"],
  failure: ["no-var", "var-on-top", "linebreak"],
  skipped: ["no-extra-semi", "no-dup-keys"]
};
function makeList(arr) {
  // Only change code below this line
  const failureItems = [];
  // Only change code above this line

  return failureItems;
}

const failuresList = makeList(result.failure);
```

- The above function 'makeList(arr)' already has a variable 'failureItems' declared with an empty array.
- Use a 'for loop' to iterate through the object 'results'
  
  ```js
  for (let i = 0; i < arr.length; i++) 
  ```

  - Just to recap on for loops, the above loop has variable 'i' assigned with '0'.
  - While the index value of 'i' is less than the length of the entire array,
  - '1' will be added to the index value of 'i' to increment through the array.

  ```js
  for (let i = 0; i < arr.length; i++) {
    failureItems.push(`<li class="text-warning">${arr[i]}</li>`);
  }
  ```

  - ```console.log(makeList(result.failure))``` will execute the function for the duration based on the parameters defined in the for loop
  - Based on the arguments passed through the function, the function will iterate through the 'failure' array in the 'results' object.
  - It will then push the elements of the array ```<li class="text-warning">${arr[i]}</li>``` to the empty array (```failureItems = []```) in sequence.
  - NOTE: DO NOT enter 'return' INSIDE the function scope. It will terminate the loop on its first pass and return only the first element of the array. When using a loop, the return statement must be OUTSIDE of the function to ensure that the loop iterates through the entire array specified.

The solution is shown below.

```js
const result = {
  success: ["max-length", "no-amd", "prefer-arrow-functions"],
  failure: ["no-var", "var-on-top", "linebreak"],
  skipped: ["no-extra-semi", "no-dup-keys"]
};
function makeList(arr) {
  // Only change code below this line
  const failureItems = [];
  for (let i = 0; i < arr.length; i++) {
    failureItems.push(`<li class="text-warning">${arr[i]}</li>`);
  }
  // Only change code above this line

  return failureItems;
}

const failuresList = makeList(result.failure);
```

Just to go over this code verbally.

- When 'function makeList(arr)' is executed, it declares a variable 'failureItems' with an empty array.
- The function will iterate through the array specified in the argument (in the above case, it is the 'failure' property in the 'results' object) for the duration of the loop specified.
- The values extracted from the loop are stored in the call stack.
- It is returned to the empty 'failureItems' array with the class attribute and its value specified in the ```<li></li>``` tag when the return statement outside of the function is executed.

### Write concise object literal declarations using object property shorthand

- ES6 allows the use of object property shorthand which eliminates redundancy.

For example

```js
const getMousePosition = (x, y) => ({
    x: x,
    y: y
});
```

- When ```function getMousePosition(34, 54);``` is called, the arguments passed through the function will be assigned to the respective property.
- The names of the argument parameters become the property name, and the arguments passed through the function becomes the values of those respective properties.

But using object property shorthand makes the above code simpler.

```js
const getMousePosition = (x, y) => ({
    x, 
    y
});
```

- Simply writing 'x' and 'y' once in the return portion will automatically convert it into 'x: x' and 'y: y', respectively.

Another example.

```js
const createPerson = (name, age, gender) => {
    // Only change code below this line
    return {
        name: name,
        age: age,
        gender: gender
    };
    // Only change code above this line
};
```

- Following the logic of the previous example, all you need to do is remove the colons and the redundant words, like so.

```js
const createPerson = (name, age, gender) => {
    return {    // return ({
        name,   //      name,
        age,    //      age,
        gender  //      gender
    };          // });  Both are acceptable.
};
```

- In the above two codes, ```console.log(createPerson("Josh", 43, "male));``` will display ```{name: 'Josh', age: 42, gender: 'male'}```
- NOTE: The curly braces in the return portion of the function can be wrapped in parentheses.
  - It is a technique used to indicate that the expression within the parentheses is an object and should be returned by the function.
  - It has no effect of the output. It is optional and sometimes added for clarity and improved readability.
- NOTE: The above code format is called a 'block body syntax' of arrow function.
  - It requires an explicit 'return' statement in order to return the object literal.

There is another way to write the code above using 'concise body syntax' of arrow function.

```js
const createPerson = (name , age, gender) => ({
    name, 
    age,
    gender
});
```

- The above uses the 'concise body syntax' of arrow function.
  - The difference is that the curly braces after the arrow function are wrapped in parentheses.
  - it automatically returns the expression given after the '=>'
  - it does not require a 'return' statement.
  - it is used when a single expression is returned.

#### Side-note on Destructuring Assignment used with arrow function

- Destructuring assignment is a way to extract values from arrays or objects and assign them to new variables.
- When destructing assignment is used on the left side of the arrow function (=>)
  - Allows you to extract values from an object/array and ```assign``` them as ```function parameters```.
  - Makes it easier to write functions that accept complex data structures.
- When it is used on the right side of the arrow function
  - Allows you to extract values from an object/array and ```return``` them as an ```object literal```.
