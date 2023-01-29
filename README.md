# ES6 - ECMAScript

## FCC - ES6 module learning journal

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

#### Mutate an array declared with const

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
