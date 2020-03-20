# State & Lifecycle
* Key goal: abstract away the implementation details of component states
* State is private, and fully controlled by component

**Local state in class**:
```javascript
class Clock extends React.Component {
    constructor(props) {
        // Class components should always call base constructor with props
        super(props);

        // Create new local variable/state
        // 'state' has a special meaning
        this.state = {date: new Date()};
    }

    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>The time is: {this.state.date.toLocaleTimeString()}</h2>
            </div>
        )
    }
}
```

## Lifecycle
* **Mounting**: Component rendered to the DOM for the first time
* **Unmounting**: DOM produed by component removed

**Clock ticking example**:
```javascript
class Clock extends React.Component {
    constructor(props) {
        super(props);

        // State initialization
        this.state = {date: new Date()};
    }

    // Lifecycle method for mounting
    componentDidMount() {
        // Tick every 1s
        this.timerID = setInterval(
            () => this.tick(),
            1000
        );
    }

    // Lifecycle method for unmounting
    componentWillUnmount() {
        // Tear down the timer
        clearInterval(this.timerID);
    }

    tick() {
        // Update state to an object with one field of the date.
        // Calling new Date() gives Date with current time.
        // State updating occurs here.
        this.setState({
            date: new Date()
        });
    }

    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>The time is: {this.state.date.toLocaleTimeString()}</h2>
            </div>
        )
    }
}
```

## State Guidelines
**Do not modify state directly**
```javascript
// Incorrect; Will not re-render component
// Can only assign state in the constructor
this.state.name = 'A';

// Correct
this.setState({name: 'A'});
```

**State updates may be asynchronous**
* Multiple `setState()` calls may be batched into single update for performance
* Should not rely on `props` or `state` values for calculating next state, since they may be update asynhronously!
* Fix by using `setState()` that accepts function instead of object

```javascript
// Incorrect
this.setState({
    counter: this.state.counter + this.props.add,
});

// Correct
this.setState((state, props) => ({
    counter: state.counter + props.add
}));
```

**State updates are merged**
* Upon calling `setState()`, object provided is **merged** into current state.
* Merging is shallow: leaves unspecified values in-tact, but completely replaces specified value.

```javascript
constructor(props) {
    super(props);
    this.state = {
        posts: [],
        comments: []
    };
}

// ...

// Posts are updated independently of comments.
// Comments are kept in-tact, whille posts are completely replaced.
this.setState({
    posts: newPosts
});
```

## Data Flow Down
* State is local/encapsulated (not accessible to any component other than the one that owns it)
* Component may pass its state down as props to child components
* The child component wouldn't know if the attribute received comes from state, props or was typed in.
* **Top-down**/**unidirectional** data flow: Any state is always owned by some specific component, and any data or UI derived from that state can only affect components **below** them in the tree.
* Stateless components can be used inside stateful components, and vice versa.

```javascript
// State passed down from parent component to child component
<FormattedDate date={this.state.date}>
```

# Events
* Function passed in as **event handler** rather than string

**DOM vs JSX**:
```html
<!-- DOM -->
<button onclick="playVideo()">
  Play Video
</button>

<!-- JSX -->
<button onClick={playVideo}>
  Play Video
</button>
```

**Preventing default behavior**:
```javascript
// ...
```