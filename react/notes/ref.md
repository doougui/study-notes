# Ref

## What's the difference between a ref and a state?

- “remember” some information, but don’t trigger new renders.
- intentionally mutable.
- Unlike state, ref is a plain JavaScript object with the current property that you can read and modify.
- When a piece of information is used for rendering, keep it in state. When a piece of information is only needed by event handlers and changing it doesn’t require a re-render, using a ref may be more efficient.

## When to use refs 

Typically, you will use a ref when your component needs to “step outside” React and communicate with external APIs—often a browser API that won’t impact the appearance of the component. Here are a few of these rare situations:

- Storing timeout IDs
- Storing and manipulating DOM elements, which we cover on the next page
- Storing other objects that aren’t necessary to calculate the JSX.

If your component needs to store some value, but it doesn’t impact the rendering logic, choose refs.

## When React attaches the refs 

React sets ref.current during the commit. Before updating the DOM, React sets the affected ref.current values to null. After updating the DOM, React immediately sets them to the corresponding DOM nodes.

## How to force React to update (“flush”) the DOM synchronously?

Import flushSync from react-dom and wrap the state update into a flushSync call:

```js
flushSync(() => {
  setTodos([ ...todos, newTodo]);
});
listRef.current.lastChild.scrollIntoView();
```
