# Unhandled Promise Rejection in Express.js Route Handler

This repository demonstrates a common yet subtle error in Node.js Express.js applications: unhandled promise rejections in asynchronous request handlers.  If an error occurs within an asynchronous operation *before* the response is sent, the error is silently swallowed, leading to unexpected behavior.

The `bug.js` file showcases this issue.  The `bugSolution.js` file provides a corrected version demonstrating how to properly handle errors.

## How to Reproduce

1. Clone this repository.
2. Navigate to the repository's directory in your terminal.
3. Run `npm install` to install the required dependencies.
4. Run `node bug.js`.  Observe the server's behavior and console output.
5. Run `node bugSolution.js` to see the corrected behavior.

## Problem and Solution
The problem arises because the `catch` block within the asynchronous operation is executed only after the promise resolves, but the response has not yet been sent and is not available to send an error. The solution involves ensuring proper error handling at a higher level to handle this. The correct solution is to use a centralized error handler that intercepts the request errors before the response is sent. The solution also includes sending error responses to the client.