# Debugging in Node

**REDO SCREENSHOTS**

## Learning Goals

* Use the Node.js debugger

## Introduction

While `console.log()` is a valuable debugging tool, it only gets us so far. When
we start running JavaScript code in the browser, we will have access to the
browser's debugger. The debugger allows you to set [breakpoints][] in your code
that will stop the execution of the code at that point. You can then inspect the
values of your variables at that point in your code.

We will start running JavaScript in the browser a bit later in the course. In
the meantime, Node.js (which is the _runtime environment_ that enables us to run
our JavaScript outside the browser) includes a similar debugging tool. In this
lesson, we will walk through how to use the [Node.js debugger][node-debugger].

Fork and clone this lesson into your local environment. Navigate into its
directory in the terminal, then run `code .` to open the files in Visual Studio
Code. There are no tests so you do not need to run `npm install`.

## The Node.js Debugger

Open `index.js` and take a look. You will see we have created a simple `while`
loop that `console.log()`s a message. Run `node index.js` to see it in action.

Using the debugger is a simple matter of adding the `debugger` keyword at the
point in our code where we want to place a breakpoint (i.e., where we want to
pause execution). Modify the code in `index.js` as follows:

```js
let count = 1;
while (count < 5) {
  debugger;
  if (count === 1) {
    console.log(`This loop has executed ${count} time.`);
  } else {
    console.log(`This loop has executed ${count} times.`);
  }
  count += 1;
}
```

To start the debugger, run `node inspect index.js`. You should see this in your
terminal:

![enter debugger](https://curriculum-content.s3.amazonaws.com/phase-0/debugging-in-node/enter-debugger.png)

Next, enter `cont` at the `debug` prompt to start executing the code. You will
see a `>` pointing to line 3, indicating that the execution of the code has been
stopped at that point:

![start execution](https://curriculum-content.s3.amazonaws.com/phase-0/debugging-in-node/start-execution.png)

Now say we want to check the value of our `count` variable. To do that, we need
to enter the debugger's REPL by running `repl`. You will now have a `>` prompt
in place of the `debug>` prompt. Type in `count` to see the current value of the
variable:

![enter repl](https://curriculum-content.s3.amazonaws.com/phase-0/debugging-in-node/enter-repl.png)

Then to continue executing the code, we first need to exit the REPL by typing
`Ctrl-C`, then run `cont` at the `debug` prompt:

![second loop](https://curriculum-content.s3.amazonaws.com/phase-0/debugging-in-node/second-loop.png)

Note that our logged message shows at the top of the screenshot above. When we
ran `cont`, the execution of the code resumed so the `console.log()` was run,
the `count` variable was incremented, and the execution contined to the next
loop. If you enter the REPL and check the value of `count`, you will see that
it's now equal to `2`.

But what if we wanted to check the value  of `count` both before _and_ after the
incrementation? We can simply add a second breakpoint:

```js
let count = 1;
while (count < 5) {
  debugger;
  if (count === 1) {
    console.log(`This loop has executed ${count} time.`);
  } else {
    console.log(`This loop has executed ${count} times.`);
  }
  count += 1;
  debugger;
}
```

In order for the debugger to recognize the change to our code, we'll need to
exit and restart it. If you're in the REPL, type `ctrl-C` to exit that, then
type `.exit` at the `debug` prompt or `ctrl-C` twice to exit the debugger.
Finally, run `node inspect index.js` to relaunch the debugger.

Now if you run `cont`, the code will beginning executing and will pause at the
first breakpoint. To continue executing the code and advance to the second
breakpoint, simply enter `cont` again. At any point, you can enter the
debugger's REPL to check the value of `count`, then exit the REPL and continue
execution of the code.

## Conclusion

In this lesson we've learned about using the debugger built in to Node.js. To
review, the process is as follows:

* Place one or more breakpoints in your code using the `debugger` keyword
* Run `node inspect <filename>` in the terminal to launch the debugger
* Run `cont` at the `debug` prompt to start execution of the code and advance to the first breakpoint
* Run `repl` at the `debug` prompt to enter the debugger's REPL
* Check the value of any variables by entering the variable name at the `>` prompt
* Exit the REPL using `ctrl-C`
* Continue stepping through the code using `cont`
* Run `.exit` or type `ctrl-C` twice to exit the debugger

We will get more practice using the debugger in an upcoming lesson.

## Resources

* [W3schools - JavaScript Debugging](https://www.w3schools.com/js/js_debugging.asp)
* [Difference between Node.js and Javascript](https://www.geeksforgeeks.org/difference-between-node-js-and-javascript/)

[breakpoints]: https://en.wikipedia.org/wiki/Breakpoint
[node-debugger]: https://nodejs.org/api/debugger.html
