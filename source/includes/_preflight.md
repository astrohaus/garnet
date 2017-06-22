## Preflight Extensions

> Register a *Preflight* in `index.js`:

```javascript
  register('preflights/openpgp.js', {
    type: 'preflight',
    folder: 'a'  // only use this Preflight for folder A
  });
```

> Return the new Document object, a Promise, or null:

```javascript
function(document, user, modules){
  let openpgp = modules.opengpg;
  openpgp.initWorker();

  return 
    fetch('extension://my-extension-name/public_key.txt')
    .then((response) => {
      return response.text();
    })
    .then((public_key) => {
      let options = {
        data: document.body,
        publicKeys: openpgp.key.readArmored(pubkey).keys
      }
      return openpgp.encrypt(options)
    })
    .then(function(ciphertext) {
      return ciphertext.data;
    });
}
```

A *Preflight* extension performs an operation on a document just before uploading the document to Postbox.

The *Preflight* extension receives these arguments:

Position | Argument | Type | Description
-------- | --------- | ---- | -----------
1 | document | object | A document object
2 | user | object | A user object
3 | modules | object | An object exporting several third-party libraries for use in extensions

A *Preflight* extension must return one of the following values:

Type | Example | Description
---- | ------- | -----------
String | 'new text' | A complete text buffer of the document body
Object | `{body: 'new text', data: {}}` | A Document object
Promise | `fetch().then((obj) => {return obj})` | A Promise object
Null | `null` | A `null` return value will be ignored; the document will not be uploaded.
