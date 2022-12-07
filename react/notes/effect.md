## What's the difference between an event and an effect

Effects let you specify side effects that are caused by rendering itself, rather than by a particular event. Sending a message in the chat is an event because it is directly caused by the user clicking a specific button. However, setting up a server connection is an Effect because it needs to happen regardless of which interaction caused the component to appear. Effects run at the end of the rendering process after the screen updates. This is a good time to synchronize the React components with some external system (like network or a third-party library).

## Why useEffect runs twice?

Imagine the ChatRoom component is a part of a larger app with many different screens. The user starts their journey on the ChatRoom page. The component mounts and calls connection.connect(). Then imagine the user navigates to another screen—for example, to the Settings page. The ChatRoom component unmounts. Finally, the user clicks Back and ChatRoom mounts again. This would set up a second connection—but the first connection was never destroyed! As the user navigates across the app, the connections would keep piling up.

Bugs like this are easy to miss without extensive manual testing. To help you spot them quickly, in development React remounts every component once immediately after its initial mount. Seeing the "✅ Connecting..." log twice helps you notice the real issue: your code doesn’t close the connection when the component unmounts.
