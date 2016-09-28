# React Component Life Cycle

There are several React lifecycle methods that help us manage the asynchronous and non-determinate nature of a Component during it’s lifetime in an app – we need provided methods to help us handle when a component is created, rendered, updates, or removed from the DOM.

At the highest level, React components have lifecycle events that fall into three general categories:

1. Initialization
2. State/Property Updates
3. Destruction

Let’s first classify and define the life-cycle methods:

## The "Will's" - invoked right before the event represented occurs.

```componentWillMount()``` - Invoked once, both on the client and server, immediately before the initial rendering occurs. If you call setState within this method, render() will see the updated state and will be executed only once despite the state change.

```componentWillReceiveProps(object nextProps)``` - Invoked when a component is receiving new props. This method is not called for the initial render. Calling this.setState() within this function will not trigger an additional render. One common mistake is for code executed during this lifecycle method to assume that props have changed.

```componentWillUnmount()``` - Invoked immediately before a component is unmounted from the DOM. Perform any necessary cleanup in this method, such as invalidating timers or cleaning up any DOM elements that were created in componentDidMount.

```componentWillUpdate(object nextProps, object nextState)``` - Invoked immediately before rendering when new props or state are being received. This method is not called for the initial render.

## The "Did's"

```componentDidMount()``` - Invoked once, only on the client (not on the server), immediately after the initial rendering occurs. At this point in the lifecycle, you can access any refs to your children (e.g., to access the underlying DOM representation). The componentDidMount() method of child components is invoked before that of the parent component.

```componentDidUpdate(object prevProps, object prevState) - Invoked immediately after the component’s updates are flushed to the DOM. This method is not called for the initial render. Use this as an opportunity to operate on the DOM when the component has been updated.

## The "Should's"

```shouldComponentUpdate(object nextState, object nextProps)``` - Invoked before rendering when new props or state are being received. This method is not called for the initial render or when forceUpdate() is used. Use this as an opportunity to return false when you’re certain that the transition to the new props and state will not require a component update.

Having a strong understanding of how these fit together – and how ```setState()``` or ```forceUpdate()``` affect the lifecycle – will help the conscious React developer build robust UIs.