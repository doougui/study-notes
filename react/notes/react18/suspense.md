## What is the basic idea of Suspense?

Read data over the network as easily as props or state

## What is Suspense?

A React component that lets you specify in a declarative way, right inside your jSX, that when a part of the UI is not ready, we want to show something different in the meantime.

## What Suspense solves

- It makes loading states more declarative
- It lets us treat other asynchronous dependencies in a similar way we want to treat data.
  - We are not limited to using Suspense just for data, it could be used to control the loading states for any type of async resource we need to load.