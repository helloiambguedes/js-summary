# Understanding Promises in JavaScript
Check:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

## Table of Contents
1. [What is a Promise?](#what-is-a-promise)
2. [Creating a Promise](#creating-a-promise)
3. [Promise States](#promise-states)
4. [Handling Promises](#handling-promises)
5. [Chaining Promises](#chaining-promises)
6. [Error Handling](#error-handling)

## What is a Promise?
A Promise is an object that represents the eventual completion or failure of an asynchronous operation. It can be in one of three states:
- Pending: The initial state, neither fulfilled nor rejected.
- Fulfilled: The operation completed successfully, and a result is available.
- Rejected: The operation failed, and an error reason is available.

## Creating a Promise
To create a Promise, you use the `new Promise()` constructor. It takes a single argument, a function with two parameters, `resolve` and `reject`. 

```javascript
const fetchData = new Promise((resolve, reject) => {
  // Simulate a network request
  setTimeout(() => {
    const data = { message: "Data fetched successfully" };
    resolve(data); // Resolve the Promise with data
  }, 2000);
});
```

## Promise States
As mentioned earlier, Promises have three possible states. You can access the current state using the `then`, `catch`, or `finally` methods. Here's how you can check the state of a Promise:

```javascript
fetchData.then((result) => {
  // Fulfilled state
  console.log("Fulfilled:", result);
}).catch((error) => {
  // Rejected state
  console.error("Rejected:", error);
});
```

## Promise States
As mentioned earlier, Promises have three possible states. You can access the current state using the then, catch, or finally methods. Here's how you can check the state of a Promise:

```javascript
fetchData.then((result) => {
  // Fulfilled state
  console.log("Fulfilled:", result);
}).catch((error) => {
  // Rejected state
  console.error("Rejected:", error);
});
```

## Handling Promises
You can use the then method to handle the successful resolution of a Promise and the catch method to handle errors. Additionally, the finally method allows you to execute code regardless of whether the Promise is fulfilled or rejected.

```javascript
fetchData
  .then((result) => {
    console.log("Fulfilled:", result);
  })
  .catch((error) => {
    console.error("Rejected:", error);
  })
  .finally(() => {
    console.log("Cleanup or final actions here");
  });
```

## Chaining Promises
Promises can be chained to execute asynchronous operations sequentially. This is helpful when you need to perform multiple asynchronous tasks in a specific order. Use the then method to chain Promises.

```javascript
fetchData
  .then((result) => {
    // Process data
    return processResult(result);
  })
  .then((processedData) => {
    // Do something with the processed data
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Error Handling
In the event of an error within a Promise, you can use the reject function to signal failure and provide an error message or object. It will trigger the catch block for error handling.

```javascript
const fetchDataWithError = new Promise((resolve, reject) => {
  // Simulate an error
  setTimeout(() => {
    reject("Error fetching data");
  }, 2000);
});```