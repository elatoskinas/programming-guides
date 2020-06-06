# Events
* Events in C# follow the Publisher-Subscriber model.
* The **publisher** invokes these events, and **subscribers** listen to these events.
* *Key benefit:* The publisher is not aware of the subscribers, so a clear separation of concerns can be
achieved.

## Delegates
* Type that represents references to methods with a particular parameter list and return type

**Declaration & invoking**
```c#
// Define delegate
public delegate void TriggerDelegate(int arg);

// Define event (instance of TriggerDelegate)
public event TriggerDelegate OnTriggerEvent;

// Invoke event with the single argument
OnTriggerEvent.Invoke(2);
```

**Subscribing & unsubscribing**
```c#
void someFunc(int arg) {
    // do something
}

// Subscribe someFunc as callback when event gets triggered
OnTriggerEvent += someFunc

// Unsubscribe someFunc to no longer trigger it when event invokedS
OnTriggerEvent -= someFunc
```

### Events vs Delegates
* Events in C# are a type of delegate
* To use an Event, a delegate must be defined first.
* Event is a wrapper on the Delegate type
* Problem with delegates: Delegate properties can easily be overwritten, which leads to errors.
Thus, Event should be used instead to avoid problems.

## EventHandler
* Delegate of the form `public delegate void EventHandler(object sender, EventArgs e);`
* Generally a standard for system events

**Declaration & invoking**
```c#
// Declaration of EventHandler
public event EventHandler onEventTriggered;

// Invoke event with no event args and sender object
onEventTriggered.Invoke(sender, EventArgs.Empty);
```

**Subscribing & unsubscribing**
```c#
// Subscription same as event in delegate
void func1(object sender, EventArgs e) {
    // do something
}

// Subscribe
onEventTriggered += func1

// Unsubscribe
onEventTriggered -= func1
```

**Arguments**
```c#
// Class for EventArgs
public class OnTriggerEventArgs : EventArgs {
    public int number;
}

// Event that returns OnTriggerEventArgs as arguments
public event EventHandler<OnTriggerEventArgs> OnTrigger;

// Invoke event with arguments
OnTrigger.Invoke(sender, new OnTriggerEventArgs { number = 3 });

// Callback with event args
void func2(object sender, OnTriggerEventArgs e) {
    // ...
}
```

## Actions
* Delegate that returns void
* Shorthand for: `public delegate void Action<T>(T obj)`

```c#
// Definition
public event Action<int, float> OnActionEvent;

// Invoking
OnActionEvent.Invoke(3, 2f);

// Subscription is the same as for EventHandler
void actionCallback(int a1, float a2) {
    // do something
}

OnActionEvent += actionCallback;
OnActionEvent -= actionCallback;
```

## Unity: UnityEvent
* Advantage: Visible in editor
* Disadvantage: Less efficient

```c#
// Declaration (note no event keyword)
public UnityEvent<int> OnUnityEvent;

// Invoking
OnUnityEvent.Invoke();

// Subscription/desubscription generally done in editor
```