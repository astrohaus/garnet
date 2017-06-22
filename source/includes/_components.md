## Components

> Register a component in `index.js`:

```javascript
  register('components/character-generator.js', {
    type: 'console'
  });
  register('components/canvas.js', {
    type: 'canvas',
    folder: 'a'
  });
  register('components/file-manager.js', {
    type: 'component'
  });
```

> Example:

```javascript
function(modules) {
    return class MyComponent extends modules.React.Component {
        constructor() {
            super()

            this.state = {
                visible: false
            }

            this.onHotkey_bound = this.onHotkey.bind(this);
        }

        onHotkey(event){
            if(event.key === 'm'){
                this.setState({
                    visible: !this.state.visible
                });
            }
        }

        componentWillUnmount() {
            this.props.emitter.off('hotkey', this.onHotkey_bound);
        }

        componentDidMount() {
            this.props.emitter.on('hotkey', this.onHotkey_bound);
        }

        render() {
            if(!this.state.visible){
                return modules.React.createElement('span');
            }
            return modules.React.createElement('div', { 
                style: {
                    position: 'fixed',
                    width: '25%',
                    right: '0px',
                    top: '0px',
                    height: '100%',
                    border: '1px solid black',
                    backgroundColor: 'white'
                }
            }, 'My Text');
        }
    };
}
```

The *Console*, *Canvas*, and *Component* extensions are user interface elements that are added to the Freewrite application.

A *Console* extension adds a new status bar to the lower console on a Freewrite.

A *Canvas* extension replaces the text editor for a provided folder.

A *Component* extension is injected to application and can respond to certain events to make itself visible or hidden.

### Properties

Components are written using React. (JSX support may be available in the future.)

Certain properties are passed to the component and can be accessed through `this.props`:

Property | Description
-------- | -----------
`emitter` | An event emitter used to bind to Freewrite events like `hotkey`
`data` | An object containing extension data

### Actions

Actions are also passed to components and can be accessed through `this.props.actions`:

Action | Description
------ | -----------
`patchExtensionData({...})` | Updates `this.props.data` available to all extension components
`putExtensionData({...})` | Overwrites `this.props.data` available to all extension components

These two `patch/put` actions can update data across multiple components registered in the same extension.

### Event Emitter

An event emitter is provided for listening to and emitting events.

Subscriber Events | Arguments | Description
----- | --------- | -----------
`hotkey` | `event` | Emits an `event` object containing `event.key` which represents a `NEW+{key}` hotkey press.
`document.load` | `document` | 

Publisher Events | Arguments | Description
----- | --------- | -----------
`document.select` | | 
`document.new` | | 
`document.prev` | | 
`document.next` | | 
`block.create` | | 
`block.update` | | 
`block.delete` | | 
`language.cycle` | | 
`toggle-frontlight` | | 



### Upcoming Events (not implemented yet)

* Add `emitter.promise(...)` convenience method for emitting event with promised callback
* `document.list`