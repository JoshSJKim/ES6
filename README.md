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
