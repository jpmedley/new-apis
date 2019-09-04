# Contact Picker API

The Contact Picker API provides a browser-based user interfaces that allows websites to gain one-off access to a user's contact information while letting the user retain full control over the shared data. 

## Contact Picker API Concepts and Usage

## Interfaces

<dl>
  <dt>ContactsManager</dt>
  <dd>Provides a means of prompting users to select one or more contacts.</dd>
  <dt>navigator.contacts</dt>
  <dd>Returns the <code>ContactsManager</code> interface.</dd>
</dl>

## Examples

```js
if ('contacts' in navigator && 'ContactsManager' in window) {
  const props = ['name', 'email', 'tel'];
  const opts = { multiple: true };
  
  try {
    const contacts = await navigator.contacts.select(props, opts);
    handleResults(contacts);
  } catch (err) {
    // Handle any errors.
  }
} else {
  // Do something else.
}
```

## Specifications

[Contact Picker API](https://wicg.github.io/contact-api/spec/)