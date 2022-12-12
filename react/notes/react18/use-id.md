# [useId](https://reactjs.org/docs/hooks-reference.html#useid)

useId is a hook for generating unique IDs that are stable across the server and client, while avoiding hydration mismatches.

useId is not for generating keys in a list. Keys should be generated from your data.

Example:

```js
function NameFields() {
  const id = useId();
  return (
    <div>
      <label htmlFor={id + '-firstName'}>First Name</label>
      <div>
        <input id={id + '-firstName'} type="text" />
      </div>
      <label htmlFor={id + '-lastName'}>Last Name</label>
      <div>
        <input id={id + '-lastName'} type="text" />
      </div>
    </div>
  );
}
```