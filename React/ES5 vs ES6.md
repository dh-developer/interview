# ES5 vs ES6 Differences

Creating React Components the ES5 way involves using the React.createClass() method:

```
var Comments = React.createClass({

    displayName: 'Comments',

    getInitialState: function(){
        return {comments: []}
    },

    getDefaultProps: function(){
        return {some_object: {a:1, b:2, c:3}}
    },

    _handleClick: function(){
        alert('hello world!')
    },

    render: function(){
        return <div>
            There are {this.state.comments.length} comments
            <button onClick={this._handleClick}>click me!</button>
        </div>
    }
})
```

This Comments Component can now be rendered either inside another React Component or directly in the call to ReactDOM.render():

```ReactDOM.render(<Comments />, document.querySelector('.app'))```

ES5 Components have some particular qualities, which we'll note:

Like the above example, to set the state to an initial value, create the getInitialState() function on the Component. What it returns will be the initial state for a Component when rendered.

Additionally, you can set the default props for the component to have a certain value with the getDefaultProps() method on the ES5 version.

The displayName is used in debugging and error reporting by React. If you use JSX, then the displayName is automatically filled out.

For some, it is common practice to denote a custom method added to a React Component by prefixing it with an underscore, hence _handleClick. _handleClick is passed as the onClick callback for a button in the code above. We can't do this so easily in the ES6 API of React, because the ES5 version has autobinding, but the ES6 does not. Let's take a look at what autobinding provides:
Auto-binding

Consider the following piece of code:

```
var thing = {
    name: 'jen',
    speak: function(){ console.log(this.name) }
}

window.addEventListener('keyup', thing.speak)
```

Invoking thing.speak() in the console will log "jen", but pressing a key will log undefined because the context of the callback is the global object. The browser's global object – window – becomes this inside the speak() function, so this.name becomes window.name, which is undefined.

React in ES5 automatically does autobinding, effectively doing the following:

```window.addEventListener('keyup', thing.speak.bind(thing))```

Autobinding automatically binds our functions to the React Component instance so that passing the function by reference in the render() works seamlessly.

Creating React Components the ES6 way works a little differently, favoring the ES6 class ... extends ... syntax, and no autobinding feature:

```
class Comments extends React.Component {
    constructor(props){
        super(props)
        this.state = {comments: []}
    }

    _handleClick(){
        alert('hello world!')
    }

    render(){
        return <div>
            There are {this.state.comments.length} comments
            <button onClick={() => this._handleClick}>click me!</button>
        </div>
    }
}
Comments.defaultProps = {a:1, b:2, c:3}
Comments.displayName = 'Comments'
```

1. Notice that in ES6, we have a constructor() that we use to set the initial state.  
2. We can add default props and a display name as properties of the new class created.  
3. The render() method, which works as normal, but we've had to alter how we pass in the callback function. This current approach (<button onClick={() => this._handleClick}>click me!</button>) will create a new function each time the component is re-rendered; so if it becomes a performance bottleneck, you can always bind manually and store the callback:

```
class Comments extends React.Component {
    constructor(props){
        super(props)
        // this._handleClick = this._handleClick.bind(this)
    }
    // ...
    render(){
        return <button onClick={this._handleClick}> click me! </button>
        // or
        return  <button onClick={this._handleClick.bind(this)}> click me! </button>
    }
}
```

Many React utility libraries on npm provide a single function to bind all handlers in the constructor, just like React does:

```
class Comments extends React.Component {
    constructor(props){
        super(props)
        // this._handleClick = this._handleClick.bind(this)
    }
    // ...
    render(){
        return <button onClick={this._handleClick}> click me! </button>
        // or
        return  <button onClick={this._handleClick.bind(this)}> click me! </button>
    }
}
```
