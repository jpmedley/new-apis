# Contact Picker API

The Contact Picker API provides a browser-based user interfaces that allows websites to gain limited access to a user's contact information while letting the user retain full control over what data is shared. 

## Contact Picker API Concepts and Usage

Use cases for this API include selecting email recipients and looking up phone numbers for voice-over-IP calls.

### Feature Detection

Feature detection is accomplished by verifying the `contacts` property on `navigator`.

```js
if ('contacts' in navigator) {
  // Use the API
}
```

### Using the API

The API is a single call to `navigator.contacts.select()` that specifies the type of requested information which includes one of `"email"`, `"name"`, or `"tel"`.

```js
const props = ['name', 'email', 'tel'];
const opts = { multiple: true };

try {
  const contacts = await navigator.contacts.select(props, opts);
  console.log(contacts);
} catch (ex) {
  // Handle any errors here.
}
```

This returns a Promise and invokes the native UI's contact picker. After the user selects contacts, the Promise resolves with a JSON object containing arrays of the requested information types.

```js
[{
  "email": [],
  "name": ["Queen O'Hearts"],
  "tel": ["+1-206-555-1000", "+1-206-555-1111"]
}]
```

Access to the user's contacts is restricted to only what is returned. If the site or app needs more than what was provided, it must call `select()` again.

### The Contact Picker

As stated, calling `select()` invokes the native UI's contacts picker. It must be called with a user gesture on a secure, top-level browsing context. The picker can never be shown on page load or at random times unrelated to user input.

Per the specification, the contact picker will never have a `select all` option. This encourages sites and apps to only ask for what they need. However, if if `options.multiple` (passed to `select()`) is set to `true`, users may select multiple contacts.

other behaviors of the user interface are platform specific.

## Interfaces

<dl>
  <dt><code>ContactsManager</code> (Secure context)</dt>
  <dd>Provides a means of prompting users to select one or more contacts.</dd>
  <dt>navigator.contacts</dt>
  <dd>Returns the <code>ContactsManager</code> interface.</dd>
</dl>

## Examples

```js
if ('contacts' in navigator) {
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