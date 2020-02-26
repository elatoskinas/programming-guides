# Control Flow
Control flow constructs in Kotlin.

## Conditionals
Simple conditional:
```kotlin
val d: Int

if (a > c) {
    d = 1
} else {
    d = 0
}
```

Expression:
```kotlin
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```