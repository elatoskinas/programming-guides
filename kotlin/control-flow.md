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

## When
```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1 -> "One"
        2 -> "Two"
        3 -> "Three"
        3.14f -> "Pi"
        is Long -> "Long"
        !is String -> "Not a string"
        else -> "Unknown"
    }

println(describe(1)) // One
println(describe(3.14f)) // Pi
println(describe("x")) // Unknown
```

## Loops
### For
```kotlin
val items = listOf("A", "B", "C")

// For-each loop
for (item in items) {
    println(item)
}

// For loop with indices
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```

### While
```kotlin
var index = 0

while (index < 5) {
    println(index)
    index++
}
```