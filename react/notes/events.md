# Events

## What's the difference between passing funcitons and calling functions?

Passed funcitons:
```js
<button onClick={handleClick}>
```

- Only calls the function when the user clicks the button

Called functions:
```js
<button onClick={handleClick()}>
```

- Fires the function immediately during rendering
- This is because JavaScript inside the JSX { and } executes right away.

## How to capture all events on child elements regardless of stopped propagation

- You can use `onClickCapture`

```js
<div onClickCapture={() => { /* this runs first */ }}>
  <button onClick={e => e.stopPropagation()} />
  <button onClick={e => e.stopPropagation()} />
</div>
```

- Capture events are useful for code like routers or analytics, but you probably won’t use them in app code.

## Can event handlers have side effects? 

- Absolutely! Event handlers are the best place for side effects.

- Unlike rendering functions, event handlers don’t need to be pure, so it’s a great place to change something—for example, change an input’s value in response to typing, or change a list in response to a button press. However, in order to change some information, you first need some way to store it. In React, this is done by using state, a component’s memory. You will learn all about it on the next page.
