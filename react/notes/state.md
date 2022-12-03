# State

## What's the difference between local variables and states?

Local variables:
```js
export function Component() {
  let index = 0;

  function handleClick() {
    index = index + 1;
  }

  return <button onClick={handleClick}>Increment</button>;
}
```

The code above won't work because:
- Local variables don’t persist between renders. When React renders this component a second time, it renders it from scratch—it doesn’t consider any changes to the local variables.
- Changes to local variables won’t trigger renders. React doesn’t realize it needs to render the component again with the new data.

Contrary to local variables, useState:
- Retain data between renders
- Triggers re-renders when the setter is called

## What are hooks?

- Hooks are special functions that are only available while React is rendering. They let you “hook into” different React features.
- Hooks—functions starting with use—can only be called at the top level of your components or your own Hooks. You can’t call Hooks inside conditions, loops, or other nested functions. Hooks are functions, but it’s helpful to think of them as unconditional declarations about your component’s needs. You “use” React features at the top of your component similar to how you “import” modules at the top of your file.

## Render and Commit

- Step 1: Trigger a render 
  - Initial render (createRoot)
  - State has updated (setState function)
    - Queues a render

- Step 2: React renders your components 
  - “Rendering” is React calling your components
  - If the updated component returns some other component, React will render that component next, and if that component also returns something, it will render that component next, and so on

- Step 3: React commits changes to the DOM 
  - React only changes the DOM nodes if there’s a difference between renders