# Basics
Building blocks:
* **Elements**
* **Components**

## JSX
* Produces React **elements**
* Any valid JS expression can be put inside curly braces

**Embedding expressions**:
```javascript
const name = 'John Doe';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
)
```

**JSX as an expression**:
```javascript
function getGreeting(user) {
    if (user) {
        return <h1>Hello, {user}!</h1>;
    }
    return <h1>Hello, Stranger</h2>
}
```

**Specifying attributes in DOM**:
```javascript
const literalAttribute = <div attrib="0"></div>;
const expressionAttribute = <div attrib={attribute}></div>;
```

**Various syntax details**:
```javascript
// Empty tags can be closed immediately with />
const element = <img src={url} />

// Specifying children
const elementWithChildren = (
    <div>
        <h1>Heading 1</h1>
        <h2>Heading 2</h2>
    </div>
);

// Injection attacks are prevented in JSX
// Below is safe; React DOM escapes values embedded
// in JSX before rendering them.
const content = response.content;
const element2 = <p>{content}</p>
```

## Elements
* Smallest building blocks. Elements make up components, and are used to construct the DOM.
* Essentially descriptions of what is seen on the screen
* React elements are immutable
* React DOM only applies the DOM updates neccessary to bring DOM to desired state

```javascript
// The following two examples are identical

const element = (
    <h1 className="greeting">
    Hello, world!
    </h1>
);

const element2 = React.createElement(
    'h1',
    {className: 'greeting'},
    'Hello, world!'
)
```

**Rendering element into DOM**:
```javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('id'));
```

**Ticking clock example**:
```javascript
function tick() {
    const element = (
        <div>
            <h1>Hello world!</h1>
            <h2>The time is: {new Date().toLocaleTimeString()}.</h2>
        </div>
    );
    
    // Only updates what's neccessary, rather than the entire DOM element
    ReactDOM.render(element, document.getElementById('id'));
}

setInterval(tick, 1000);
```

## Components
* Allows splitting UI into modular pieces, allowing to think about each piece in isolation
* Arbitrary inputs (props) are accepted by components, and React elements describing what should appear on the screen are returned
* **All React components must at like pure functions with respect to their props (input should not be changed)**

**Function component**:
```javascript
// Valid React component, since it:
// 1.Accepts a single props (properties) object
// 2.Returns a React element

function Welcome(props) {
    return <h1>Hello, {props.name}</h1>
}
```

**Class components**:
```javascript
// Equivalent to function component in previous example

class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>
    }
}
```

**Rendering a component**:
```javascript
// Define function component
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

// Name gets passed into props
const element = <Welcome name="John Doe" />;

// Welcome component gets rendered with {name: 'John Doe'} as props
ReactDOM.render(
    element,
    document.getElementById('id')
)
```

**Composing components**:
```javascript
// Components can refer to other components in their output

// Create smaller component
function Number(props) {
    return <h1>Number: {props.number}</h1>;
}

// Build larger component from smaller ones
function List() {
    return (
        <div>
            <List number="1" />
            <List number="2" />
            <List number="3" />
        </div>
    );
}

ReactDOM.render(
    <List />,
    document.getElementById('id')
)
```


## Conventions
* Attributes in elements written in `camelCase`
* Component names start with a **capital letter**