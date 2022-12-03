# React keys

Why are they needed?
  - Imagine that files on your desktop didn’t have names. Instead, you’d refer to them by their order — the first file, the second file, and so on. You could get used to it, but once you delete a file, it would get confusing. The second file would become the first file, the third file would be the second file, and so on.
  - File names in a folder and JSX keys in an array serve a similar purpose. They let us uniquely identify an item between its siblings. A well-chosen key provides more information than the position within the array. Even if the position changes due to reordering, the key lets React identify the item throughout its lifetime.

Why shouldn't you use `index` as key?
  - You might be tempted to use an item’s index in the array as its key. In fact, that’s what React will use if you don’t specify a key at all. But the order in which you render items will change over time if an item is inserted, deleted, or if the array gets reordered. Index as a key often leads to subtle and confusing bugs.
  - Similarly, do not generate keys on the fly, e.g. with key={Math.random()}. This will cause keys to never match up between renders, leading to all your components and DOM being recreated every time. Not only is this slow, but it will also lose any user input inside the list items. Instead, use a stable ID based on the data.

# Pure and unpure components

What is the difference between pure components and unpure components
  - Characteristics
    - It minds its own business. It does not change any objects or variables that existed before it was called.
    - Same inputs, same output. Given the same inputs, a pure function should always return the same result.
  - Pure components will always return the same output (JSX) given the same inputs.
  - It's just like a pure function in math
    - Consider this math formula: y = 2x.
    - If x = 2 then y = 4. Always.
  - Example of unpure component
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

Detecting impure calculations with StrictMode
  - When you want to change something in response to user input, you should set state instead of writing to a variable. You should never change preexisting variables or objects while your component is rendering.
  - React offers a “Strict Mode” in which it calls each component’s function twice during development. By calling the component functions twice, Strict Mode helps find components that break these rules.
  - Notice how the original example displayed “Guest #2”, “Guest #4”, and “Guest #6” instead of “Guest #1”, “Guest #2”, and “Guest #3”. The original function was impure, so calling it twice broke it. But the fixed pure version works even if the function is called twice every time. Pure functions only calculate, so calling them twice won’t change anything—just like calling double(2) twice doesn’t change what’s returned, and solving y = 2x twice doesn’t change what y is. Same inputs, same outputs. Always.