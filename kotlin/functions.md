# Functions
## Basics

Standard function:
```kotlin
fun func(a: Int, b: Int): Int {
    return a + b
}
```

Expression body and type inference:
```kotlin
fun sum(a: Int, b: Int) = a + b
```

Void equivalent (return type can be ommitted):
```kotlin
fun hello(): Unit {
    println("Hello world!)
}
```