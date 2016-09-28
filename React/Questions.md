# Question 1: Explain this Code

Given the code below, answer the following questions -

```
class MyComponent extends React.Component {
    constructor(props) {
        // set the default internal state
        this.state = {
            clicks: 0
        };
    }

    componentDidMount() {
        this.refs.myComponentDiv.addEventListener(
            ‘click’, 
            this.clickHandler
        );
    }

    componentWillUnmount() {
        this.refs.myComponentDiv.removeEventListener(
            ‘click’, 
            this.clickHandler
        );
    }

    clickHandler() {
        this.setState({
            clicks: this.clicks + 1
        });
    }

    render() {
        let children = this.props.children;

        return (
            <div className=”my-component” ref=”myComponentDiv”>
                <h2>My Component ({this.state.clicks} clicks})</h2>
                <h3>{this.props.headerText}</h3>
                {children}
            </div>
        );
    }
}
```

### Can you identify two problems in the code above?

1. The constructor does not pass its props to the super class. It should include the following line:

    ```
    constructor(props) {
            super(props);
            // ...
        }
    ```

2. The event listener (when assigned via addEventListener()) is not properly scoped because ES2015 doesn’t provide autobinding. Therefore we might re-assign clickHandler in the constructor to include the correct binding to this:

    ```
    constructor(props) {
        super(props);
              this.clickHandler = this.clickHandler.bind(this);
        // ...
    }
    ```

### Can you explain what the output of this class actually does? How would you use it in an application?

This class creates a ```<div />``` element and attaches a click listener to it. The content of this component includes a ```<h2 />``` element that updates every time the user clicks on the parent ```<div />```, as well as an ```<h3 />``` element containing a provided title and whatever child elements were passed to it.

To use this class, we would import it into another class and use it like this:

```
<MyComponent headerText=”A list of paragraph tags”>
    <p>First child.</p>
    <p>Any other <span>number</span> of children...</p>
</MyComponent>
```
