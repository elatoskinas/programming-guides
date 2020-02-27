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

Auto-cast to non-nullable
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
### Numbers
Declarations:
```kotlin
val one = 1 // Int
val oneLong = 1L // Long
val oneShort: Short = 1 // Short
val oneByte: Byte = 1 // Byte
val oneFloat = 1f // Float
val oneDouble = 1.0 // Double

val longValue = 3000000000 // Automatically assigned Long type
val bigNumber = 1_000_000 // Can use underscorers to make numbers more readable

val bin = 0b0000101 // 5
val hex = 0x00000ff // 255
```

Max & min values:
```kotlin
println("${Int.MAX_VALUE}, ${Int.MIN_VALUE}")       // 2^31 - 1, -2^31
println("${Long.MAX_VALUE}, ${Long.MIN_VALUE}")     // 2^63 - 1, -2^63
println("${Float.MAX_VALUE}, ${Float.MIN_VALUE}")   // 9223372036854775807, -9223372036854775808
println("${Double.MAX_VALUE}, ${Double.MIN_VALUE}") // 3.4028235e38, 1.4e-45
println("${Byte.MAX_VALUE}, ${Byte.MIN_VALUE}")     // 2^7 - 1 (127), -2^7
```

Boxing
```kotlin
val a: Int = 10000
val boxedA: Int? = a
val boxedA2: Int? = a

println(a === a) // True
println(boxedA == boxedA2) // True; Equality preserved
println(boxedA === boxedA2) // False; Identity not preserved
```

Conversions:
```kotlin
val b: Byte = 1 // Valid (literals are checked statically)
// val i: Int = b // Throws error (cannot assign different number type)

val i: Int = b.toInt() // Valid. Byte explicitly widened.

// Arithmetical operations are overloaded for appropriate conversions.
val l = 1L + 3 // Long + Int => Long
```

Valid conversions:
- `kotlin toByte(): Byte`
- `kotlin toShort(): Short`
- `kotlin: toInt(): Int`
- `kotlin: toLong(): Long`
- `kotlin: toFloat(): Float`
- `kotlin: toDouble(): Double`
- `kotlin: toChar(): Char`

Operations:
` + - * / %`

```kotlin
val x = 5 / 2 // 2
val y = 5 / 2.toDouble() // 2.5

// Bitwise operators (Int and Long only)
val b1 = 1 shl 2 // Shift left: 4
val b2 = 8 shr 3 // Shift right: 1
val b3 = 2 ushr 3 // Unsigned shift right: 0
val b4 = 7 and 3 // Bitwise AND: 0111 & 0011 = 0011 = 3
val b5 = 16 or 8 // Bitwise OR: 1000 | 0100 = 1100 = 24
val b6 = 21 xor 5 // Bitwise XOR: 10101 ^ 00101 = 10000 = 16
val b7 = 3.inv() // Flip bits of 3: -4
```

Comparisons:
`a == b`, `a != b`, `a < b`, `a > b`, `a <= b`, `a >= b `

`equals` and `compareTo` special cases:
- `NaN` considered equal to itself
- `NaN` considered greater than any other element including `POSITIVE_INFINITY`
- `-0.0` is considered less than `0.0`

#### Unsigned Integers (experimental)
`UByte`, `UShort`, `UInt`, `ULong`

```kotlin
val b: UByte = 1u
val s: UShort = 1u
val l: ULong = 1u
val a1 = 42u // UInt (since constant fits in UInt)
val a2 = 0xFFFF_FFFF_FFFFu // ULong (since constant does not fit in UInt)
val a3 = 1UL // ULong
```

### Characters
Characters & Numbers:
```kotlin
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9')
        throw IllegalArgumentException("Out of range)
    return c.toInt() - '0'.toInt() // Explicit conversion to numbers
}

// Charracters cannot be treated directly as numbers
val c: Char = 'c'

// Will throw error, since Char and Int incompatible types
if (c == 3) {
    // ...
}
```

Escape sequences:
- `\t`: Tab
- `\b`: Backscape
- `\n`: Newline
- `\r`: Carriage Return
- `\'`, `\"`, `\\`, `\$`

### Booleans
Values: `true`, `false`
Operators: `||, &&, !`

### Arrays
`Array` class
```kotlin
val array = arrayOf(1, 2, 3) // [1, 2, 3]
val nullArray = arrayOfNulls<Int>(4) // [null, null, null, null]
val lambdaArray = Array(5) { i -> (i * i) } // 0, 1, 4, 9, 16

// Specialized array classes
val intArray: IntArray = intArrayOf(4, 6, 7)       // [4, 6, 7]
val shortArray: ShortArray = shortArrayOf(9, 1, 2) // [9, 1, 2]
val byteArray: ByteArray = byteArrayOf(2, 2, 3)    // [2, 2, 3]
val intArrayZeros: IntArray = IntArray(4)          // [0, 0, 0, 0]
```

### Strings
Strings are immutable.

Escaped & Raw Strings:
```kotlin
// Escaped String (may have escaped characters in them)
val s = "Hello World!\n"

// Raw strings
// (no escaping and can containg newlines and any other characters)
val text = """
    for (c in "foo")
        print(c)
"""
```

Operations:
```kotlin
val str = "abc"
val strChar = str[1] // 'b' (second character)
val concat = str + 2 + 'c' // abc2c

// Will print a, b and then c on newlines
for (c in str) {
    println(c)
}

// Removes leading whitespace
val text = """
    |Lorem ipsum
    |A B C
    |D
""".trimMargin()

println(text)
```

String templates:
```kotlin
val str1 = "num: $num" // num: 4

val str2 = "${str1.replace("num", "number")} !" // number: 4 !

// Arbitrary expression
val s = "abcde"
val str3 = "$s.length is ${s.length}" // abcde.length is 5

val str4 = "${'$'}10" // Escaping dollar sign
```

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
```

Automatic cast:
```kotlin
// No need to cast explicitly
if (obj is String && obj.length > 0) {
    return "Length: $obj.length"
}
```