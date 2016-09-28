# JSX

When Facebook first released React to the world, they also introduced a new dialect of JavaScript called JSX that embeds raw HTML templates inside JavaScript code. JSX code by itself cannot be read by the browser; it must be transpiled into traditional JavaScript using tools like Babel and webpack. While many developers understandably have initial knee-jerk reactions against it, JSX (in tandem with ES2015) has become the defacto method of defining React components.

```
class MyComponent extends React.Component {
    render() {
        let props = this.props;

        return (
            <div className="my-component">
                <a href={props.url}>{props.name}>/a>
            </div>
        );
    }
}
```

If you are asked this question during an interview, it is ultimately asking you to state an informed opinion towards JSX and defend it based on personal experience. Let’s cover some of the basic talking points.

### Key Talking Points

Developers do not have to use JSX (and ES2015) to write an application in React.

This is certainly true. Having said that, many React developers prefer to use JSX as its syntax is far more declarative and reduces overall code complexity. Facebook certainly encourages it in all of their documentation!

Adopting JSX allows the developer to simultaneously adopt ES2015 — giving immediate access to some wonderful syntactic sugar.

ES2015 introduced a variety of new features to JavaScript that makes writing large applications far easier than ever before: classes, block scoping via let, and the new spread operator are just a small portion of the additions.

```
import AnotherClass from ‘./AnotherClass’;

class MyComponent extends React.Component {
    render() {
        let props = this.props;

        return (
            <div className="my-component">
                <AnotherClass {...props} />
            </div>
        );
    }
}
```

But while ES2015 is becoming more and more widespread, it still is far from widely supported by the major browsers — so you’ll need to use a tool like Babel or webpack to convert everything into legacy ES5 code.

If you have built a React application using JSX and ES2015, be sure to speak about some specific pros or cons you encountered:

Although it took me some time to get used to the JSX and ES2015 syntax, I discovered how much I really enjoyed using it. Specifically, I’m a big fan of...

On the other hand, I could do without the hassle of configuring webpack and Babel. Our team ran into issues with...