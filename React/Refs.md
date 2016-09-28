# React Refs

Similarly to keys, refs are added as an attribute to a ```React.createElement()``` call, such as ```<li ref="someName"/>```. The ref serves a different purpose, it provides us quick and simple access to the DOM Element represented by a React Element.

Refs can be either a string or a function. Using a string will tell React to automatically store the DOM Element as ```this.refs[refValue]```. For example:

```
class List extends Component {
    constructor(p){
        super(p)
    }

    _printValue(){
        console.log(this.refs.someThing.value)
    }

    render() {
        return <div onClick={e => this._printValue()}>
            <p>test</p>
            <input type="text" ref="someThing" />
        </div>
    }
}

DOM.render(<List />, document.body)
```

this.refs.someThing inside componentDidUpdate() used to refer to a special identifier that we could use with ```React.findDOMNode(refObject)``` – which would provide us with the DOM node that exists on the DOM at this very specific instance in time. Now, React automatically attaches the DOM node to the ref, meaning that ```this.refs.someThing``` will directly point to a DOM Element instance.

Additionally, a ref can be a function that takes a single input. This is a more dynamic means for you assign and store the DOM nodes as variables in your code. For example:

```
class List extends Component {
    constructor(p){
        super(p)
    }

    _printValue(){
        console.log(this.myTextInput.value)
    }

    render() {
        return <div onClick={e => this._printValue()}>
            <p>test</p>
            <input type="text" ref={node => this.myTextInput = node} />
        </div>
    }
}

DOM.render(<List />, document.body)
```