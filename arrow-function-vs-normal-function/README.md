# Arrow function VS normal function

With normal javascript functions, `this` is bound when the function is called. With arrow functions, `this` is bound to the context in which the function is originally created.

With this code

```jsx
function sayHello() {
  console.log('My name is', this.name)
}

const amy = {
  name: 'Amy',
  speak: debounce(sayHello),
}

amy.speak()
```

## Arrow function

If we implement the debounce function with arrow function: 

```jsx
function debounce(func, wait) {
  let timeout
  return (...args) => {
    const context = this // <-- global scope
    clearTimeout(timeout)
    timeout = setTimeout(() => func.apply(context, args), wait)
  }
}

// My name is undefined
```

When we call `debounce` on `sayHello`, the creation context is the global scope. Therefore, the arrow function returned from debounce is also bound to the global scope, which is undefined because there’s no `name` in the global context.

## Normal function

If we implement it with normal function:

```jsx
function debounce(func, wait) {
  let timeout
  return function(...args) {
    const context = this // <-- depends on where it is called
    clearTimeout(timeout)
    timeout = setTimeout(() => func.apply(context, args), wait)
  }
}

// My name is Amy
```

Now it works, because `this` is set during runtime.
