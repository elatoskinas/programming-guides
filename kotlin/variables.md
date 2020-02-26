# Variables
Various variable-related syntax & features in Kotlin.

## Assignment
```kotlin
val a = 2 // Assign variable with inferred type Int
a = 3 // Error! values are not mutable

val b: Int = 5 // Set type
val c: Int // Requires type when initializer is provided

var x = 1 // Variables are mutable
x = 2 // No error

val d: Int // Type required when no initializer provided
d = 4 // Assignment can be deferred
//d = 3 // Error!
```

## Null safety
Nullable vs. Non-nullable:
```kotlin
fun nonNullable(a: Int): Int {
    // Invalid! Value is not nullable.
    return null
}

// Question mark ? represents nullable
fun nullable(a: Int): Int? {
    if (a > 5)
        return a
    else
        // Valid, as return type is nullable
        return null
}
```

Auto-cast to n
```kotlin
fun useNull(a: Int, b: Int) {
    val num1 = nullable(a)
    val num2 = nullable(b)

    if (num1 == null) {
        return
    }

    if (num2 == null) {
        return
    }

    // num1 and num2 auto-cast to non-nullable after null checks
    println("$num1, $num2")
}
```

## Types
### Type Checking
Standard type checking:
```kotlin
    if (obj is Int) {
        // ...
    }

    // Check that object is not of type
    if (obj !is Float) {
        // ...
    }
}
```

Automatic cast:
```kotlin
    // No need to cast explicitly
    if (obj is String && obj.length > 0) {
        return "Length: $obj.length"
    }
```



### String templates
```kotlin
val str1 = "num: $num" // num: 4
val str2 = "${str1.replace("num", "number")} !" // number: 4 !
```