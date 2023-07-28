# Collections
Various collections in Kotlin.

## Ranges
Range definition:
```kotlin
val range = 1..9 // Range: 1,2,3,4,...,9 (inclusive)
```

Checking range containment:
```kotlin
val x = 5
val y = 4
val z = 7

// Will print the result, as ranges are inclusive:
if (x in 1..y+1) {
    println("In range!")
}

// Will print the result, as 7 is not in range [1,5]
if (z !in 1..x) {
    println("Not in range!")
}
```

Iterating over range:
```kotlin
// Prints numbers from 1 to 7 inclusive
for (x in 1..7) {
    print(x)
}
```

Iterating over progression:
```kotlin
// Prints even numbers less than or equal to 14:
// 0, 2, 4, 6, 8, 10, 12
for (x in 0..12 step 2) {
    print(x)
}

// Prints even multiples of 3 in the range [0, 9] (in reverse order)
// 12, 9, 6, 3, 0
for (x in 12 downTo 0 step 3) {
    print(x)
}
```

## In keyword
Iterating over collection:
```kotlin
val items = listOf("A", "B", "C")

// Will print A, B and then C
for (item in items) {
    println(item)
}
```

Checking if collection contains object:
```kotlin
val items = listOf("D", "B")

// Will return "B contained in collection", as "B" is in items.
val result = when {
    "A" in items -> "A contained in collection"
    "B" in items -> "B contained in collection"
    else -> "No A or B found!"
}
```

## Lambda expressions
Filtering:
```kotlin
val list = listOf("a", "b", "aa", "aaa", "ca")

// Result: ["a", "aa", "aaa"]
val filtered = list.filter { it.startsWith("a") }
```

Sorting:
```kotlin
val numbers = listOf(7, 3, 1, 4, 5)

// Result: [1, 3, 4, 5, 7]
val sorted = numbers.sortedBy { it }
```

Map:
```kotlin
val nums = listOf(5, 3, 2, 4)

// Result: [25, 9, 4, 16]
val squared = nums.map { it*it }
```

ForEach:
```kotlin
val strings = listOf("hello", "world", "!")

// Result: "Prints hello world !"
strings.forEach { print("$it ")}
```

Chaining lambdas:
```kotlin
val digits = listOf(0,1,2,3,4,5,6,7,8,9)

// Result: Prints 4, 5, 6, 7
digits.filter{ it in 2..5 } // Filter to [2, 5]
        .map { it + 2 } // Add 2 to each element
        .forEach{println(it)} // Print each element
```