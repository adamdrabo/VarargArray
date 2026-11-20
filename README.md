# VarargAndArrays

Kotlin practice exercises on `vararg` parameters and arrays.

## Concepts covered

- `vararg`: lets a parameter receive a variable number of arguments (zero, one or many). The caller decides how many to pass.
  - Inside the function, the `vararg` parameter is an array.
  - A function can only have one `vararg` parameter, usually placed last.
  - The spread operator `*` passes an existing array to a `vararg` function: `sum(*values)`.
- Arrays: a fixed-size data structure that holds several values of the same type.
  - The first element is at index 0. The last one is at index `size - 1`.
  - Accessing an index that doesn't exist crashes the program.
  - An array declared with `val` can still be modified: `val` only prevents reassigning the variable.
  - `println(array)` does not show the content. Use `contentToString()` instead.
  - Useful members: `size`, `first()`, `last()`, `contains()`, `indices`, `sum()`, `min()`, `max()`, `average()`, `sorted()`.

## Exercise 1: Average (vararg)

Calculate the average of the marks entered by the user. Invalid inputs are ignored, and calling the function without arguments returns `0.0`.

```kotlin
fun main() {
    println("Enter 3 different marks")

    println("Enter mark 1: ")
    val markOne = readln().toDoubleOrNull()

    println("Enter mark 2: ")
    val markTwo = readln().toDoubleOrNull()

    println("Enter mark 3: ")
    val markThree = readln().toDoubleOrNull()

    val result = average(markOne, markTwo, markThree)
    println("The average mark is ${"%.2f".format(result)}")

    println("Average without marks: ${"%.2f".format(average())}")
}

fun average(vararg grades: Double?): Double {
    val validGrades = grades.filterNotNull()

    if (validGrades.isEmpty()) return 0.0

    return validGrades.sum() / validGrades.size
}
```

## Exercise 2: Temperatures of the week (arrays)

Analyze the temperatures of the week: minimum, maximum, average, number of days below zero, and the temperature of a day chosen by the user.

```kotlin
val temperatures = arrayOf(-3, 2, 5, -1, 0, 4, 7)

println("Min temp: ${temperatures.min()}\u00B0C -- Max temp: ${temperatures.max()}\u00B0C")

val avg = temperatures.average()
println("Average temp: ${String.format("%.2f", avg)}\u00B0C")

var daysUnderZero = 0
for (temp in temperatures) {
    if (temp < 0) {
        daysUnderZero++
    }
}
println("Number of days under 0: $daysUnderZero")

println("Enter a day number (1 to 7): ")
val day = readln().toIntOrNull()

if (day != null && day in 1..7) {
    println("Day $day temp: ${temperatures[day - 1]}\u00B0C")
} else {
    println("Invalid day")
}
```

## What I learned

- A function should return the raw value. Formatting belongs to the display, not to the calculation.
- `"%.2f".format()` follows the computer's language settings. In French, it writes a comma, and converting it back with `toDouble()` crashes the program.
- Dividing two `Int` drops the decimals. `average()` returns a `Double` and avoids this trap.
- Day 1 matches index 0, so the index of a day is `day - 1`.
- Checking `day != null && day in 1..7` protects against both invalid text and an index out of bounds.