---
tree_title: Background jobs
description: Background jobs
last_modified: 2021-10-11
---

# Background jobs

## Contents

-   [Delayed tasks and long-running processes](#delayed-tasks-and-long-running-processes)

## Delayed tasks and long-running processes

It is possible to use Redis, which is usually used as a "cache" layer in front of an app, as a job task queue and delayed "notification" system.

-   **Need an order to expire in 15 mins?** Use `bull.js` with Redis to create a job that runs after 15mins.
-   **Need to quickly respond to a request but make long-running tasks later?** Append them to `bull.js` queue and it will callback later to perform them.
