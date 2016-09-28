# React Keys

Keys in React are used to identify unique VDOM Elements with their corresponding data driving the UI; having them helps React optimize rendering by recycling existing DOM elements. Let’s look at an example to portray this.

We have two <TwitterUser> Components being rendered to a page, drawn in decreasing order of followers:

```
-----------
| A - 103 |
-----------
-----------
| B - 92  |
-----------
```

Let’s say that B gets updated with 105 Twitter followers, so the app re-renders, and switches the ordering of A and B:

```
-----------
| B - 105 |
-----------
-----------
| A - 103 |
-----------
```

Without keys, React would primarily re-render both <TwitterUser> Elements in the DOM. It would re-use DOM elements, but React won’t re-order DOM Elements on the screen.

With keys, React would actually re-order the DOM elements, instead of rendering a lot of nested DOM changes. This can serve as a huge performance enhancement, especially if the DOM and VDOM/React Elements being used are costly to render.

Keys themselves should be a unique number or string; so if a React Component is the only child with its key, then React will repurpose the DOM Element represented by that key in future calls to render().

Let’s demonstrate this with a simple list of todos rendered with React:

Interactive code sample available on Matthew Keas’ github.

```
class List extends Component {
    constructor(p){
        super(p)
        this.state = {
            items: Array(5).fill(1).map((x,i) => ({id:i}))
        }
    }

    componentDidMount(){
        const random = (a,b) => Math.random() < .5 ? -1 : 1

        setInterval(() => {
            this.setState({
                items: this.state.items.sort(random)
            })
        }, 20)
    }

    render() {
        let {items} = this.state
        return <ul>
            {items.map(item =>
                <li key={item.id}>{item.id}</li>)}
        </ul>
    }
}

DOM.render(<List />, document.body)
```

The setInterval() occurring on mount reorders the items array in this.state every 20ms. Computationally, if React is reordering the items in state, then it would manipulate the DOM elements themselves instead of “dragging” them around between positions in the ```<ul>```.

It is worth noting here that if you render a homogenous array of children – such as the ```<li>```’s above – React will actually ```console.warn()``` you of the potential issue, giving you a stack trace and line number to debug from. You won’t have to worry about React quietly breaking.