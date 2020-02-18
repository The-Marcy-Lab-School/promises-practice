# Unit 6 Lesson 1 Practice: Promises

## Directions
Fork and clone this lab. Respond to questions in clear, concise sentences directly within this markdown file.

**1. What will the following code snippet log? Why?**
  ```javascript
  console.log('Line 1')
  setTimeout(() => console.log('Line 2'), 1000)
  console.log('Line 3')
  ```
  + This snippet logs `Line 1`, then `Line 3`, and finally `Line 2` after one second. This is because `setTimeout` is a asynchronous function that lets JavaScript move on to the next line of code while it waits for the correct time to execute.

**2. What does the following code snippet log? Why?**
  ```javascript
  function createPromise(seconds) {
    return new Promise((resolve) => {
      setTimeout(function() {
        resolve(`After ${seconds} second(s), this promise is resolved.`)
      }, seconds * 1000)
    })
  }

  console.log(createPromise(1))
  ```
  + This snippet does not log text to the console. This occurs because `createPromise` returns a promise object that after its resolved, after `setTimeout` runs, but doesn't do much in its `resolve` condition.

**3. How do we use our `createPromise` function to log `"After 1 second(s), this promise is resolved."`**
  + In order to log this statement to the console, we can add a `.then()` statement to our promise that receives the data passed by `resolve` and can log it.

**4. What does the following code snippet return? What does it log?**
  ```javascript
  const ourPromise = new Promise((resolve) => {
    resolve(12);
  })

  ourPromise.then(value => value * 2);
  ```
  + This snippet logs `24` because our `then()` statement can see the `12` that is passed when the promise is fulfilled.

**5. What does the following code snippet return? What does it log?** <br> **Note: Instead of using the `Promise` constructor to create a Promise that immediately resolves to 12, we can just use the [`Promise.resolve`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) method.**
  ```javascript
  const ourPromise = Promise.resolve(12);
  ourPromise.then(value => value * 2).then(value => value + 10);
  ```
  + This snippet returns `34` because `Promise.resolve` returns a promise like our previous snippets and then the resolve value of `12` is manipulated by the `then()` statements.

**6. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => console.log(value + 10))
  ```
  + This snippet logs `34` as well. This is different because the resolution of the promise is not captured by any variable, and the `then()` statements are chained to the promise.

**7. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    });
  ```
  + This code snippet first logs `34` and then returns `34`. This is different from the previous snippet because of the `return`. We might expect the snippet to return `44`, but the `log` console method did not reassign value.

**8. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.reject(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    }).catch(reason => {
      const message = `${reason} is a bad number.`;
      console.error(message);
      return reason;
    });
  ```
  + This snippet logs `12 is a bad number` and returns `12` because `Promise.reject` returns a rejected promise, meaning our `catch()` method is invoked. This `catch` statement first interpolates `12` into a string and logs it to the console, then, the number itself is returned.