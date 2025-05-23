# Array.prototype.forEach() vs For Loop

Let’s look at this example, we want to reimplement `Promise.race` — to return the fastest resolved promise among *n* promises.

There are the promises we are going to process, and the expected outcome is `3` because `p2` takes the shortest time to resolve.

```jsx
const p0 = new Promise((resolve) => {
  setTimeout(() => {
    resolve(1);
  }, 200);
});
const p1 = new Promise((resolve) => {
  setTimeout(() => {
    resolve(2);
  }, 100);
});
const p2 = new Promise((resolve) => {
  setTimeout(() => {
    resolve(3);
  }, 10);
});
```

---

### For Loop
If we use `for loop`, the code will look like:

```jsx
for (let i = 0; i < iterable.length; i++) {
  try {
    const res = await iterable[i];
    resolve(res);
  } catch (err) {
    reject(err);
  }
}

// output: 1
```
...and the output will be `1`, which is expected because for loop awaits the promise to resolve in each iteration. But this is an incorrect answer.

---

### Array.prototype.forEach()

If we use `Array.prototype.forEach()`, the code will look like:

```jsx
iterable.forEach(async (item, index) => {
  try {
    const res = await item;
    resolve(res);
  } catch (err) {
    reject(err);
  }
});
    
// output: 3
```
...and now the output is `3`, the correct answer. Why?

The reason being — according to [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#description),`forEach()` expects a synchronous function — it does not wait for promises. In other words, it will not wait for async callbacks even though we use `async` and `await`, and there’s no way to break or continue early.

For loop on the other hand, provides manual control like break and continue. It will respect to our `await` properly.
