## Assets & Data

> Register a *JSON* data fixture in `index.js`:

```javascript
  register('component.json', {
    type: 'component'
  });
  register('names.json', {
    type: 'json'
  });
```

> The data fixture `names.json`:

```javascript
{
    "names": [
        "chrono",
        "lucca",
        "marle",
        "frog",
        "magus",
        "ayla",
        "robo"
    ]
}
```

> Accessing the data in a component:

```javascript
function(modules) {
    class GeneratorComponent extends modules.React.Component {
        getRandomName(){
            // The data fixture is keyed by its filename
            let names = this.props.data['names.json']['names'];

            let index = Math.floor(Math.random() * names.length);
            return names[index];
        }
    }
}
```

> Accessing any Extension asset using `fetch`:

```javascript
fetch_secret = function(){
  fetch('extension://secretSauce/secret.txt')
  .then((response) => {
    console.log(response.text());
  });
}
```

Data fixtures can be loaded by registering a file path as a `json` extension type. JSON data loaded this way will be available to all components included in the extension and accessible through `this.props.data`.

Alternatively, any asset can be loaded asynchronously by using the fetch API (example at right).