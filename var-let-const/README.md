# **Hoisting**

- `var` variables are hoisting, meaning they will get moved to the top of their scope and initialized as `undefined`, so we can use them before the declarations.
- `let` and `const` are non-hoisting, JavaScript forbids any use of the variables declared with let and const before its declaration. We will see `ReferenceError` if we try to do so. This limitation is also called [**Temporal dead zone (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz).**

<aside>
💡 Hoisting is a JavaScript mechanism where the interpreter appears to move the *declaration* of functions, variables, classes, or imports to the top of their scope, before the code execution. https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
</aside>

<aside>
💡 Variables declared with `let`, `const`, or `class` is said to be in a [**Temporal dead zone (TDZ)**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz) from the start of the block until code execution reaches the place where the variable is declared and initialized.
</aside>

# Assignment

- We can declare `var` variables again and change their values.
- We can change `let` variables' values but can't declare them again.
- `const` can't be declared again or have its value changed.