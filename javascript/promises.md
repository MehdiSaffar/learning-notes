---
tree_title: Promises & Async
description: All things related to Promises and asynchronous programming
last_modified: 2021-10-11
---

# Promises & Async

## Contents

-   [Single or multi-threaded?](#single-or-multi-threaded)
-   [Defer pattern (or antipattern?)](#defer-pattern-or-antipattern)

## Single or multi-threaded?

The main Javascript execution context is single-threaded, NOT multithreaded. The underlying engine however can be (and I think IS) multithreaded.

The event loop merely gives the illusion of things happening in parallel, however at any point in time only a single piece of code runs. 

If we take the example of an async with say 3 `await` points, we can roughly think of that function's code as being broken down to 4 "contiguous pieces of synchronous code", which we can call Tasks.

Each task runs in one go until completion. When we hit an await, the function takes a "break" and the engine chooses another task to run. 

So it is akin to having multiple processes running on a single core, and the OS schedule execution. However, what is important to remember, is that Javascript tasks run until completion, while the OS runs until pre-emption.

## Defer pattern (or antipattern?)

It is possible to create a Promise that can be resolved "externally" and "manually" - that is, from outside the `(resolve, reject) => {...}` callback.

It looks like this:

```javascript
// https://lea.verou.me/2016/12/resolve-promises-externally-with-this-one-weird-trick/

module.exports = function defer() {
    let res
    let rej

    const promise = new Promise((resolve, reject) => {
        res = resolve
        rej = reject
    })

    promise.resolve = res
    promise.reject = rej

    return promise
}
```

This is called a Deferred pattern and is actually discouraged from use when using Promises, however there might a time it is needed so it is good to know.
