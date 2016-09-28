# React Interview Questions

### What is React?

React is an open-source JavaScript library created by Facebook for building complex, interactive UIs in web and mobile applications.

* What makes React a good tool and what are the parts of it you don't like.
* Talk about projects you've used it for and why was the decision made?
* Describe life cycle [[more](Component Lifecycle.md)]
* How do you prefer to split up components?
* What can you tell me about JSX? [[more](JSX.md)]
* Explain the Virtual DOM, and a pragmatic overview of how React renders it to the DOM.
* What is the significance of refs in React? [[more](Refs.md)]
* What is the significance of keys in React? [[more](Keys.md)]
* What are stateless components? [[more](Stateless.md)]

### What is Redux?

* How does data flow through the app when using Redux?
* How do you separate actions, reducers, and where do you prefer to dispatch actions? 
* How do you prefer to deal with asynchronous actions? (What about Auth issues where have to reAuth and try again?)

Most people can study those questions, so we like to put an emphasis on their thoughts and experiences with Redux or React. What was the most challenging aspect? Setting up the folder structure? Redux boilerplate? Random React/JSX specific errors? Nesting components? Passing functions and props around? Deploying? Setting up webpack, hot reloader, styles? This generally gives a better sense that they've used the tool and have a deep understanding instead of spending a week memorizing the documentation.

### How would you solve jQuery vs React boundary for network requests?

Let's say you are using a jQuery library.  How would you organize the code and integrate it with React?  (obviously unidea solution)

### ES5 vs ES6

What are the advantages and disadvantages of using one or the other?  Include notes about default props, initial state, PropTypes, and DisplayName. [[more](ES5 vs ES6.md)]

### React-Router library

* When would you use this library?
* How would you use this to create an experience like below where 
** Only ONE page shows at a time depending on which link was clicked on
** Active page link must be highlighted

```
<nav>
	<li>Home</li>
	<li>People</li>
	<li>About</li>
</nav>
<div class="contents">
	<div id="Home" class="page"><!--Home content--></div>
	<div id="People" class="page"><!--People content--></div>
	<div id="About" class="page"><!--About content--></div>
</div>

```

### Problems With Below Code

Identify two problems with the code below [[more](Questions.md)]  

```
class MyComponent extends React.Component {
    constructor(props) {
        // set the default internal state
        this.state = {
            clicks: 0
        };
    }
    ...
}
 ```

1. The constructor does not pass its props to the super class. It should include the following line:

    ```super(props); // missing from constructor```

2. The event listener (when assigned via ```addEventListener()```) is not properly scoped because ES2015 doesn't provide autobinding. Therefore we might re-assign clickHandler in the constructor to include the correct binding to this:

    ```this.clickHandler = this.clickHandler.bind(this)``` 


# Resources

* https://www.codementor.io/reactjs/tutorial/5-essential-reactjs-interview-questions
* https://www.toptal.com/react/interview-questions
* https://www.reddit.com/r/reactjs/
* https://www.reddit.com/r/reactjs/comments/54xnao/fat_arrow_vs_autobind_vs_bindbindbindbindbind/