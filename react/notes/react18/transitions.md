# [Transitions](https://reactjs.org/blog/2022/03/29/react-v18.html#new-feature-transitions)

## What is it?

A transition is a new concept in React to distinguish between urgent and non-urgent updates.

- Urgent updates reflect direct interaction, like typing, clicking, pressing, and so on.
- Transition updates transition the UI from one view to another.

You can use startTransition API inside an input event to inform React which updates are urgent and which are “transitions”:

```js
import {startTransition} from 'react';

// Urgent: Show what was typed
setInputValue(input);

// Mark any state updates inside as transitions
startTransition(() => {
  // Transition: Show the results
  setSearchQuery(input);
});
```

Updates wrapped in startTransition are handled as non-urgent and will be interrupted if more urgent updates like clicks or key presses come in. If a transition gets interrupted by the user (for example, by typing multiple characters in a row), React will throw out the stale rendering work that wasn’t finished and render only the latest update.

useTransition: a hook to start transitions, including a value to track the pending state.
startTransition: a method to start transitions when the hook cannot be used.

Additional links:
- [https://youtu.be/WtiF3DP6oWk?t=702](https://youtu.be/WtiF3DP6oWk?t=702)
- [React 18 useTransition Hook Crash Course](https://youtu.be/N5R6NL3UE7I)