# Stateless Components

If React components are essentially state machines that generate UI markup, then what are stateless components?

Stateless components (a flavor of “reusable” components) are nothing more than pure functions that render DOM based solely on the properties provided to them.

```
const StatelessCmp = (props) => {
    return (
        <div className=”my-stateless-component”>
            {props.name}: {props.birthday}
        </div>
    );
};

// ---
ReactDOM.render(
    <StatelessCmp name=”Art” birthday=”10/01/1980” />,
    document.getElementById(“main”)
);
```

As you can see, this component has no need for any internal state — let alone a constructor or lifecycle handlers. The output of the component is purely a function of the properties provided to it.