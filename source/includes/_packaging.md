## Creating an Extension package

> Here is an example `package.json`:

```json
{
  "name": "offline-folder",
  "description": "This extension disables uploading documents for a single folder."
  "sdk_versions": [
    "1.0"
  ]
}
```

> To register a file path as an extension:

```javascript
// index.js
function(sdk_version, register){ 
  register('preflights/openpgp.js', {
    type: 'preflight',
    folder: null, // optional
  });

  register('components/hint-modal.js', {
    type: 'component',
    triggers: {
      hotkey: 'z'
    },
    assets: [
      'stylesheets/style.css' // not implemented yet. use fetch API.
    ]
  });
}
```

An extension comprises at least two files:

* A `package.json` which describes the extension package
* An `index.js` which programatically registers the extension(s)

### package.json

To create a `package.json`, install [npm package manager](https://docs.npmjs.com/getting-started/installing-node) and perform this command in your terminal: `npm init`

The following fields are mandatory:

* `name`: A globally unique name for your package
* `sdk_versions: ["1.0"]`

### index.js

The `index.js` file is used to register files as extensions. You can register more than one extension in a package (e.g. both a *Preflight* extension and a *Console* extension).

The `index.js` file is invoked as an anonymous function and receives two arguments:

Parameter | Type | Description
--------- | ------- | -----------
sdk_version | String | `'1.0'`
register | Function | This is a callable function used to register file paths as extensions.

Developers can register files within their package as extensions by invoking the `register()` callable function in their `index.js`.

The first argument is a relative path to the extension's source code file. Different extension types require different values included in the second `options` argument.

Option | Required | Description
------ | -------- | -----------
type | Yes | *String*. Must be one of `preflight`, `component`, `console`, or `canvas`
folder | No | *String*. Limits the extension to being active in the given folder `a`, `b`, or `c`.
triggers | No | *Dictionary*. Register hotkeys for applicable extensions using a dictionary-like data structure.

There are four extension types available:

* Preflight
* Console
* Canvas
* Component

A *Preflight* extension modifies the document before uploading it to Postbox. This can be useful for operations like encryption.

A *Console* extension adds a new status bar component to the **console** at the bottom of your Freewrite display.

A *Canvas* extension replaces the **editor** at the top of your Freewrite display.

Finally, a *Component* extension is a custom UI element that is displayed when triggered by the user. Triggers often include custom hotkeys like `NEW` + `[Hotkey]`.