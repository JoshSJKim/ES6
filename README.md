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

- The following code can be re-written using arrow functions.

```JS
var myConcat = function(arr1, arr2) {
  return arr1.concat(arr2);
};
```

- use arrow function

```JS
const myConcat = (arr1, arr2) => arr1.concat(arr2);
```

- you can even remove the brackets for the parameters if it's a single parameter function.
- ```arr1.concat(arr2)``` can also be achieved by ```[...arr1, ...arr2]```, which is called the spread operator.

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
