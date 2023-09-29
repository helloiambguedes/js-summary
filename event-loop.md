# Understanding the Event Loop in JavaScript
Check:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop

## Introduction

The Event Loop is a core concept in JavaScript, enabling asynchronous and non-blocking behavior in web applications. It plays a crucial role in handling events, timers, and I/O operations.

## What is the Event Loop?

The Event Loop is a mechanism that allows JavaScript to perform asynchronous tasks while maintaining a responsive user interface. It manages the execution of code by continuously checking for pending tasks and executing them in a specific order. This way, JavaScript can handle tasks like handling user input, making network requests, and managing timers without blocking the main thread.

## How the Event Loop Works

The Event Loop operates in a continuous cycle, following these steps:

1. **Check the Call Stack**: The Event Loop begins by checking if the call stack is empty. The call stack is a data structure that keeps track of currently executing functions.

2. **Execute Pending Tasks**: If the call stack is empty, the Event Loop checks for pending tasks in the task queue. Tasks can include callbacks from event listeners, timers, or other asynchronous operations.

3. **Execute One Task**: The Event Loop takes the oldest task from the task queue and pushes it onto the call stack for execution.

4. **Execute the Task**: The task on the call stack is executed, which may involve running a function, handling an event, or processing a timer callback.

5. **Check for More Tasks**: After the task is completed, the Event Loop checks for more pending tasks in the queue.

6. **Repeat**: The Event Loop continues this cycle indefinitely, ensuring that asynchronous tasks are executed in the order they were added to the queue.

## Key Components of the Event Loop

Understanding some key components of the Event Loop can provide further clarity:

- **Call Stack**: The call stack is a data structure that keeps track of function calls. When a function is called, it's added to the stack, and when it returns, it's removed from the stack.

- **Task Queue**: The task queue is where asynchronous tasks are placed for execution. Events, timers, and other callbacks are added to the task queue when they are ready to be processed.

- **Microtask Queue**: In addition to the task queue, JavaScript also has a microtask queue. Microtasks have higher priority than regular tasks and are processed before regular tasks. Promises and certain APIs (like `process.nextTick` in Node.js) add microtasks to this queue.

## Example

Here's a simplified example to illustrate the Event Loop in action:

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Inside Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Inside Promise');
});

console.log('End');
```

In this example, the code is executed as follows:

1. `console.log('Start')` is added to the call stack and executed.
2. `setTimeout` and `Promise.resolve().then` are encountered, and their callbacks are scheduled to run later.
3. `console.log('End')` is added to the call stack and executed.
4. After the stack is empty, the Event Loop processes the tasks in the task queue. First, it executes the Promise microtask (`Inside Promise`) and then the timer callback (`Inside Timeout`).