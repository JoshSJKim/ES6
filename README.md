# ES6 - ECMAScript

## FCC - ES6 module learning journal

- This is the first time going through the ES6 module.
- There will be concepts and areas that I will not fully understand during the first cycle.
- I will have to cycle through this module a few more times and add to the notes as I get more acquainted with ES6.

- Run through NO.2!

### Compare scope

```JS
function checkScope() {
    let i = 'function scope';   // This variable is declared outside of the 'if' block
    if (true) {
        let i = 'block scope';  // This variable is declared inside of the 'if' block
        console.log('block scope i is: ', i); // block scope 'i' is visible only inside of the 'if' block
    }
    console.log('function scope i is: ', i);  // function scope 'i' is visible only outside of the 'if' block
    return i;   // this command will return 'function scope i' since it's placed outside of the 'if' block
}
```

- the 'i' variable defined inside the if statement is separate from the one defined within the function scope.
- ```let i = 'block scope';``` applies only within the if statement block, hence the term 'block scope'.
- ```let i = 'function scope';``` applies within the entire function, with the exception of the if statement block, where the 'i' variable is declared separately, hence the term 'function scope'.

### Mutate an array declared with const

- Remember, variables declared with 'const' keyword are read-only.
- But that doesn't mean that the contents of the value assigned to the variable declared with 'const' cannot be modified.
- Using the 'const' declaration only prevents "reassignment" of the variable identifier.

```js
const s = [5, 6, 7];
s = [1, 2, 3];  // This line will throw a TypeError. s is read-only. It cannot be reassigned with a new value or object.
```

```js
const s = [5, 6, 7];
s[2] = 45;  // This is different from reassigning a value to a variable since it's accessing an index point in the array to change the element value.
console.log(s); // [5, 6, 45]
```

- Edit the array [5, 7, 2] to [2, 5, 7]
- There are various ways to achieve this.
- You could manually assign new values to each element of the array by indexing the array.
- I think this is the intended method for this exercise.

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
- s.unshift(2) will enter the value '2' to the first element of the array (index s[0]).

Another method

```js
const s = [5, 7, 2];
function editInPlace() {
  // initialize variable 'removed' and assign it the value of removing the last value of the array 's'. The value will be stored in the call stack
  let removed = s.pop();
  // unshift (insert at index 0) the removed value to array 's'
  s.unshift(removed);       
}
editInPlace();
```

### Object Freeze

- Prevent object data mutation by applying ```Object.freeze('object_name');```

```JS
function freezeObj() {
const MATH_CONSTANTS = {
    PI: 3.14
};
Object.freeze(MATH_CONSTANTS);

try {
  MATH_CONSTANTS.PI = 99;
} catch(ex) {               // [TypeError: Cannot assign to read-only property 'PI' of object '#<object>']
  console.log(ex);
}
return MATH_CONSTANTS.PI;
}
const PI = freezeObj();
console.log(freezeObj());  // 3.14
```

### Arrow function

- Use arrow (=>) function to simplify multi-line functions to a single in-line function. This is useful when passing a function as an argument to another function.

```JS
const myFunc = function() {
    const myVar = "value";
    return myVar;
}
```

- The above code can be simplified by replacing the 'function' text to an arrow (=>) behind the parentheses, as shown below.

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

- You can pass arguments into an arrow function

```js
const doubler = (item) => item * 2;
doubler(4); // This would return 8
```

- If an arrow function has a single parameter, the parentheses can be omitted.

```js
const double = item => item * 2; // This is identical to the code above
```

- You can pass multiple arguments to an arrow function

```js
const multiplier = (item, multi) => item * multi;
multiplier(4, 2); // This would return 8
```

```JS
var myConcat = function(arr1, arr2) {
  return arr1.concat(arr2);
};
console.log(myConcat([1, 2], [3, 4, 5]));
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
console.log(greeting("Josh"));  // console will display "Hello Josh"
console.log(greeting());  // console will display "Hello Anonymous"
```

- You can set as many default values for as many parameters as needed.

Another example

- Modify the function 'increment' by adding default parameters so that it will add 1 to 'number' if value is not specified.

```js
const increment = (number, value) => number + value;
```

- If the default value of 'value' parameter is set to 1, the function will execute ```number + 1 (default)``` when value is not specified.

therefore

```js
const increment = (number, value = 1) => number + value;

console.log(increment(5)); // console will display 6.
```

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
const sum (...args) =>  args.reduce((a, b) => a + b, 0);
```

- You can think of the rest parameter as a ```blanket parameter```
- You will still need to define the function with at least one argument. (In the above code, it's 'args')
- Naming the parameter is arbitrary.

#### Side-note on array methods

Array methods have appeared in the module, but I haven't seen any detailed introduction on these methods.
So here it is.
Array methods such as map(), filter(), and reduce() are used to manipulate arrays in different ways.

##### map()

- map() is used to create a new array with the results of calling a specified function on EVERY element in the array that is called.
- The new array will have the same length as the original array.
- The new elements in the new array will be the result of the call back function applied to the original array elements.

```js
let numbers = [1, 2, 3, 4, 5];
let squaredNumbers = numbers.map(x => x * x); // x represents each element in the array. x will multiply itself by itself for each element and produce a new array
console.log(squaredNumbers);                  // console will display [1, 4, 9, 16, 25]
```

##### filter()

- filter() is used to create a new array with all elements that pass the test implemented by the provided function on the original array.
- The new array will only contain elements for which the callback function returns a 'true' response.

```js
let numbers = [1, 2, 3, 4, 5];                      // The filter method will iterate through the array and find the remainder of the value when divided by 2.
let evenNumbers = numbers.filter(x => x % 2 === 0); // if the remainder strictly equals 0, it will pass the function to be added to the new array.
console.log(evenNumbers);                           // console will display [2, 4]
```

##### reduce()

- reduce() is used to apply a function to all of the elements in the array and REDUCE it to a single value.
- The function takes two arguments: an accumulator ( the value accumulated so far), and the current value (the element being processed in the array)

```js
let numbers = [1, 2, 3, 4, 5]; 
// the reduce function will start at index '0' as specified at the end of the parentheses.
// It will iterate through the array and accumulate the sum of each element in the array.
// [(3) + [3, 4, 5]] then [(6) + [4, 5]], [(10) + [5]], etc.           
let sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum);     // console will display the sum of all of the elements in the array. [15]
```

There are other array methods commonly used in JavaScript

- concat(): concatenates two or more arrays into a new array
- slice(): returns a shallow copy of a portion of an array into a new array
- splice(): adds/removes elements from an array
- indexOf(): returns the first index at which a given element can be found in the array
- lastIndexOf(): returns the last index at which a given element can be found in the array
- join(): joins all elements of an array into a string
- reverse(): reverses the order of elements in an array
- sort(): sorts the elements of an array in place and returns the sorted array
- forEach(): executes a provided function once for each array element

- I'm sure I'll need to dive deeper into these later on.

### Spread Operator

- The spread operator uses the same syntax as the rest parameter ```(...)``` but in a different manner.
- The rest parameter is used in function definitions, whereas the spread operator is used to spread, or unpack, the elements of an iterable array or string into a new array or a new string. It can also be used to spread the properties of an object.
- It can be used in array literals, function calls, or object literals.

```JS
const arr1 = [1, 2, 3, 4, 5];
let arr2;

arr2 = [...arr1] // This is the spread operator
```

or it can be written like so

```js
const arr1 = [1, 2, 3, 4, 5];
let arr2 = [...arr1];
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
  - ```${...}``` is the template literal syntax, which is used to embed expressions into string literals.
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

### Concise declarative functions

INSTRUCTION

Refactor the function setGear inside the object bicycle to use the shorthand declarative shorthand syntax.

ES5 function

- This code works just as it is.

```js
// Only change code below this line
const bicycle = {
  gear: 2,
  setGear: function(newGear) {
    this.gear = newGear;
  }
};
// Only change code above this line
bicycle.setGear(3);
console.log(bicycle.gear);
```

ES6 function - allows you to remove the ```function``` keyword and the colon when defining functions in objects.

```js
const bicycle = {
  gear: 2,
  setGear(newGear) {  // Remove colon and keyword 'function'
    this.gear = newGear;
  }
};
```

The above two codes will display exactly the same output.

### Use class syntax to define a constructor function (requires further understanding)

- In ES6, you can create objects using the ```class``` keyword.
- In ES5, an object can be created by defining a ```constructor``` function, and the object created is instantiated by using the ```new``` keyword.
- In ES6, first the class is declared which uses a constructor method. It can be then invoked or "instantiated" using the keyword ```new```.

There are two types of constructors. Explicit and implicit

EXPLICIT

- Explicit constructor is a constructor method that is defined within the class by using the 'constructor' keyword, explicitly.
- It is then followed by a function definition, which can pass parameters of the constructor.
- When a 'instance' of the class is created using the keyword "new", the constructor is invoked, or called.
- The parameters passed through the function definition will then initialize the properties of the object.

```js
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
  takeOff() {
    console.log("To " + this.targetPlanet + "!");
  }
  }
```

- When the above is 'instantiated' like shown below,

```js
const zeus = new SpaceShuttle('Jupiter');
zeus.takeOff();
```

- it will invoke the ```class SpaceShuttle``` and pass 'jupiter' as its parameter 'targetPlanet'.
- So, when the function is called ```zeus.takeOff();```, the console will display ```"To Jupiter!"```

IMPLICIT

- Implicit constructors do not have an explicit constructor method (```constructor('something'))```)
- It is a default constructor that is created if no explicit constructor is defined within the class.
- It takes no arguments/parameters and has an empty body.
- How it behaves when it is invoked can be defined arbitrarily.

```js
class = Rocket {
  launch() {
    console.log("To the moon!");
  }
  blastOff() {
    console.log("To Mars!");
  }
}
```

- When the above is instantiated using the keyword "new"

```js
const atlas = new Rocket();
atlas.launch(); // This will print "To the moon!" in the console
atlas.blastOff(); // This will print "To Mars!" in the console
```

- Keep in mind when defining the class, UpperCamelCase should be used.

### Getters and Setters

- Getter functions are used to return (get) the value of an object's private variable to the user without the user directly accessing the private variable.
- Setter functions are used to modify (set) the value of an object's private variable based on the value passed into the setter function.
  - This function can involve calculations or overwriting the previous value.

```js
class Book {                // Define class, UpperCamelCase
  constructor(author) {     // Explicit constructor
    this._author = author;  // Conventionally, precede private variable name with an underscore.
  }    
  get writer() {            // This is the getter
    return this._author;    // The value of the private variable that will be returned when the get function is called
  }/
  set writer(updatedAuthor) {       // This is the setter
    this._author = updatedAuthor;   // The value of the private variable will be updated based on the argument passed.
  }
}

const novel = new Book('anonymous');  // 'new' keyword creates an instance of the 'Book' class and passes 'anonymous' as the argument to the constructor
console.log(novel.writer);            // This will display 'anonymous' since 'this._author' was set to 'anonymous' for 'const novel' above.
novel.writer = 'newAuthor';           // This will pass the argument 'newAuthor' to the 'updateAuthor' parameter for 'set writer' setter function.
console.log(novel.writer);            // This will display 'newAuthor' since 'this._author' was updated to 'newAuthor' using the setter above.
```

Getter Setter exercise

INSTRUCTION

- Use the class keyword to create a Thermostat class. The constructor accepts a Fahrenheit temperature.
- In the class, create a getter to obtain the temperature in Celsius and a setter to set the temperature in Celsius.
- Remember that ```C = 5/9 *(F - 32)``` and ```F = C* 9.0 / 5 + 32```, where F is the value of temperature in Fahrenheit, and C is the value of the same temperature in Celsius.

```js
// Only change code below this line
class Thermostat {                    // Define class
  constructor (fahrenheit) {          // constructor will receive temperature value in fahrenheit
    this._fahrenheit = fahrenheit;    // The argument passed through the parameter will be assigned to the private variable 'this._fahrenheit'
  }
  get temperature() {                       // getter function
    return 5/9 * (this._fahrenheit - 32);   // This formula will convert the fahrenheit value to celcius
  }
  set temperature(celcius) {                            // setter function
    return this._fahrenheit = (celcius * 9) / 5 + 32;   // This formula will convert the celcius value to fahrenheit. 
  }                                                     // The new value is assigned to 'this._fahrenheit'.
}
// Only change code above this line

const thermos = new Thermostat(76); // Receive argument in fahrenheit value
let temp = thermos.temperature; // getter function is called to return value 24.44 in Celsius
thermos.temperature = 26;   // receive celcius value and setter function is called to return 'this._fahrenheit' value in fahrenheit, which is 78.8
temp = thermos.temperature; // new fahrenheit value is assigned to 'this._fahrenheit', which is passed through the get function to return 26 in Celsius
```

- ```console.log(thermos.temperature);``` will only display results in celcius because ```get temperature()``` is defined to return values in celcius.
- When ```thermos.temperature``` is set to '26' in celcius, it looks like it goes straight to ```temp = thermos.temperature```.
  - it is actually converting the celcius value to fahrenheit, returned to 'this._fahrenheit', and when called again using the get function, it is then re-converted to celcius. Then 'temp = thermos.temperature' will be '26' in celcius again.
  - It seems redundant but it actually makes sense because the constructor is defined to receive arguments in fahrenheit.

## Create a Module Script - integrate JavaScript with HTML

```html
<html>
  <body>
    <script type="module" src="filename.js"></script>
  </body>
</html>
```

### Use export to share a code block

export syntax is also known as ```named export```.
One way to export a code block is shown below.
Assume that there is a file named ```math_functions.js```

```js
export const add = (x, y) => {  // This will export the 'add' function, which takes two arguments and return the sum of the two arguments
  return x + y;                 
}
```

The above method is a common way to export a single function. But a different method can be used to export multiple functions.

```js
const add = (x, y) => {
  return x + y;
}

const multiply = (x, y) => {
  return x * y;
}

export { add, multiply};
```

- When a variable or a function is exported, it can be imported in another file and use it without having to rewrite the code.

### Reuse JavaScript Code using import

import allows you to choose which parts of a file or module to load.

```js
import {add} from './math_functions.js';  // "import" will find 'add' in 'math_functions.js' and make it available for use.
                                          // (./) tells the import command to look for 'math_functions.jf' file in the same folder as the current file.
or                                        // relative file path(./) and file extension(.js) required when using import in this manner

import {add, multiply} from './math_functions.js';    // multiple functions or variables can be imported using the same method.
```

### Use * to import everything from a file

- ```import * as``` syntax is used to import all of the contents of the selected file in to the current file.

```js
import * as myMathModule from "./math_functions.js";
```

- The above command will import all of the exported contents from 'math_functions.js' and into an object called 'myMathModule'.
- NOTE: Only contents that have been exported will be imported.
- The object name (in this case, myMathModule), can be named anything. It is just a variable name.

### Export default and Importing a default export

- Another export syntax is known as ```export default```
- This is usually used if only one value is being exported from a file.
- It is also used to create a 'fallback' value for a file or a module.

```js
export default function add(x, y) {   // Named function
  return x + y;
}


export default function(x, y) {       // Anonymous function
  return x + y;
}
```

- export default needs to be exported on its own. It cannot be combined with other named exports.
- Once exported, it is possible to import the exported contents in a single module.

```js
export default function add(a,b) {
  return a + b;
}

export function subtract(a,b) {
  return a - b;
}

export function multiply(a,b) {
  return a * b;
}

// The above exports can be imported in a single module

import add { subtract, multiply } from './myModule.js';  
// Notice that the default export is not contained in the curly braces
// Named exports must be wrapped with '{}'.
```

- The purpose of 'export default' is to make it easier and more intuitive to import a single value from a module.
  - For example, 'export default' to export the most frequently used functions as the default export.

### JavaScript Promise

- Promise function is a constructor function.
- 'new' keyword is required to create a promise.
- It takes a function as its argument with two parameters - resolve and reject.

This is the syntax

```js
const makeServerRequest = new Promise((resolve, reject) => {});
```

- Promise has three states: pending, fulfilled, and rejected.
- The 'makeServerRequest' created above is forever stuck in the pending state because a way to complete the promise has not been defined.
- The resolve and reject parameters are used to determine if the promise is fulfilled or rejected.

#### complete a promise with resolve/reject

```js
const makeServerRequest = new Promise((resolve, reject) => {
    let responseFromServer;

    if(responseFromServer) {
      resolve("We got the data");
    } else {
      reject("Data not received");
  }
});
```

- 'responseFromServer' represents a response from a server, such as 'true' or 'false'.
- The 'if' statement will take the response 'true' or 'false'.
- if 'true', resolve method will be used to pass the string "We got the data"
- if 'false', reject method will be used to pass the string "Data not received"

#### Handle fulfilled promise with 'then'

- In the example above, makeServerRequest is waiting for a response from a server.
- if the response is true, the promise function will be resolved, and if false, it will be rejected.
- Once it receives a response from a server, something needs to be done with the response to complete the promise function

The 'then' method is used to complete the promise function.

```js
const makeServerRequest = new Promise((resolve, reject) => {
  let responseFromServer;

  if(responseFromServer) {
    resolve("We got the data") {
    } else {
    reject("Data not received");
    }
  }
});

makeServerRequest.then((result) => {
  console.log(result);
});
```

- NOTE: the 'then' method is entered outside of the promise function.
- Once a response if received from a server, let's say 'true', the 'resolve' method will be called with the string "We got the data". It indicates that the promise has been fulfilled.
- When the promise is fulfilled, the 'then' method takes a callback function as its parameter (in this case, 'result').
- The callback function ```makeServerRequest.then((result)``` takes the resolved value of the promise ("We got the data") as its parameter and logs it into the console.

##### Side-note on arrow function

- Arrow function requires that the argument list be wrapped in parentheses if there is only one argument.
- If there are no arguments, empty parentheses are still required.
- curly braces '{}' must be used to define the body of the function.
- 'then' method does not require curly braces if the code block within is a single statement.
  - However, if there are multiple statements within the code block, curly braces are required to separate the statements.
- in general, it is recommended to use curly braces at all times.

```js
makeServerRequest.then((result) => {  // argument list wrapped in parentheses. Curly braces used
  console.log(result);
});

or 

makeServerRequest.then((result) => console.log(result)); // curly braces removed. Acceptable for single statement within code block, but not recommended.
```

### Handle a rejected promise with Catch

- Up to this point, the promise function received a response, true, from the server, and using the 'then' method, took a callback function 'return' as its parameter.
- The callback function then t took the resolved value of the promise as its parameter to log it into the console "We got the data".

How about when the server returns 'false' as a response?

- The code above is capable of receiving a response 'false', but it has no means of handling the response, hence it is not able to display it into the console.
- In the same manner the 'then' method was used, the 'catch' method is used when the promise is rejected.
- It is executed immediately after a promise 'reject' is called due to receiving a 'false' response from the server.
- The syntax is exactly the same as 'then'. Just replace it with 'catch'.

```js
const makeServerRequest = new Promise((resolve, reject) => {
  let responseFromServer;

  if(responseFromServer) {
    resolve("We got the data") {
    } else {
    reject("Data not received");
    }
  }
});

makeServerRequest.then((result) => {
  console.log(result);
});
makeServerRequest.catch((error) => {
  console.log(error);
});
```

- The callback function parameter (result, error) are arbitrary and can be set to anything within the context of the code.
- As soon as 'false' is received, the reject method will be called with the string "Data not received".
- Then, the 'catch' method will take the callback function 'error', which will take the 'reject' value ("Data not received") as its parameter to log it into the console.
