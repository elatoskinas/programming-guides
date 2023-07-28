# Conditional Rendering
**Using if-statements**:
```javascript
function UserGreeting(props) {
    return <h1>Welcome back!</h1>
}

function GuestGreeting(props) {
    return <h1>Please sign u.</h1>
}

function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;

    if (isLoggedIn) {
        return <UserGreeting />
    }

    return <GuestGreeting />
}

ReactDOM.render(
    // Setting isLoggedIn to false will render GuestGreeting
    <Greeting isLoggedIn={false} />,
    // ...
)
```

**Element variables:**
```javascript
render() {
    // ...
    let greeting;

    if (isLoggedIn) {
        greeting = <UserGreeting />
    } else {
        greeting = <GuestGreeting />
    }

    // Renders either user greeting or guest gretting depending
    // on value of isLoggedIn
    return (
        <div>
            {button}
        </div>
    )
}
```

**Inline If with logical &&:**
```javascript
// Renders the h2 part (together with the h1 part) only if the first condition is met.
// Otherwise, only the h1 part is rendered.
return(
    <div>
        <h1>Hello!</h1>
        {unreadMessages.length > 0 &&
            <h2>
                You have {unreadMessages.length} unread messages.
            </h2>
        }
    </div>
)
```

**Inline If-Else with conditional operator:**
```javascript
// Render UserGreeting if isLoggedIn holds, and GuestGreeting otherwise.
// Usage of ternary if-else operator.
return(
    <div>
        {isLoggedIn
            ? <UserGreeting />
            : <GuestGreeting />}
    </div>
)
```

**Preventing component from rendering:**
```javascript
function Comp(props) {
    if (!props.condition) {
        // Hides component (prevents it from rendering)
        // This does not prevent the firing of the component's lifecycle methods.
        return null;
    }

    return <h1>Hello!</h1>;
}
```