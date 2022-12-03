# Pure and impure components

## What is the difference between pure components and impure components
  - Characteristics
    - It minds its own business. It does not change any objects or variables that existed before it was called.
    - Same inputs, same output. Given the same inputs, a pure function should always return the same result.
  - Pure components will always return the same output (JSX) given the same inputs.
  - It's just like a pure function in math
    - Consider this math formula: y = 2x.
    - If x = 2 then y = 4. Always.
  - Example of impure component
    ```jsx
    let guest = 0;

    function Cup() {
      // Bad: changing a preexisting variable!
      guest = guest + 1;
      return <h2>Tea cup for guest #{guest}</h2>;
    }

    export default function TeaSet() {
      return (
        <>
          <Cup />
          <Cup />
          <Cup />
        </>
      )
    }
    ```
    - This component is reading and writing a guest variable declared outside of it. This means that calling this component multiple times will produce different JSX! And what’s more, if other components read guest, they will produce different JSX, too, depending on when they were rendered! That’s not predictable.

## Detecting impure calculations with StrictMode
  - When you want to change something in response to user input, you should set state instead of writing to a variable. You should never change preexisting variables or objects while your component is rendering.
  - React offers a “Strict Mode” in which it calls each component’s function twice during development. By calling the component functions twice, Strict Mode helps find components that break these rules.
  - Notice how the original example displayed “Guest #2”, “Guest #4”, and “Guest #6” instead of “Guest #1”, “Guest #2”, and “Guest #3”. The original function was impure, so calling it twice broke it. But the fixed pure version works even if the function is called twice every time. Pure functions only calculate, so calling them twice won’t change anything—just like calling double(2) twice doesn’t change what’s returned, and solving y = 2x twice doesn’t change what y is. Same inputs, same outputs. Always.

## Side effects

- Side effects are changes like updating the screen, starting an animation, changing the data, etc.
- They’re things that happen “on the side”, not during rendering.
- In React, side effects usually belong inside event handlers (ex: when you click a button). Even though event handlers are defined inside your component, they don’t run during rendering! So event handlers don’t need to be pure.
- If you’ve exhausted all other options and can’t find the right event handler for your side effect, you can still attach it to your returned JSX with a useEffect call in your component. This tells React to execute it later, after rendering, when side effects are allowed. However, this approach should be your last resort.

## Why should your components be pure?

- Your components could run in a different environment—for example, on the server! Since they return the same result for the same inputs, one component can serve many user requests.
- You can improve performance by skipping rendering (memo) components whose inputs have not changed. This is safe because pure functions always return the same results, so they are safe to cache.
- If some data changes in the middle of rendering a deep component tree, React can restart rendering without wasting time to finish the outdated render. Purity makes it safe to stop calculating at any time.
