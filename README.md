# Kotlin notes

## Code style

### Expression functions

Expression functions are great tool to shorten the code. 

```kotlin
fun foo(x: String) = x.length
```

In order to keep balance between readability and usability it is not allowed to use expression functions with wrapping. If an expression function's return grows to require wrapping, use a normal function body, a `return` declaration, and normal expression wrapping rules instead.

```kotlin
// Correct - no wrapping
fun foo(x: String) =
    veryLongFunctionNameThatDoesNotFitInOneLine(x.length)
    
// Incorrect - parameters forced to use wrapping
fun foo(x: String) =
    veryLongFunctionNameThatDoesNotFitInOneLine(
        x.length,
        x.chars
    )
        
// Correct - normal function body
fun foo(x: String): Int {
    return veryLongFunctionNameThatDoesNotFitInOneLine(
        x.length,
        x.chars
    )
}
```

The rule above implies that multiline expressions are allowed (provided that they don't contain wrapping).

```kotlin
fun foo(index: Int) = when (index) {
    0 -> "foo"
    1 -> "bar"
    else -> "nothing"
}
```

Normal function body is especially desirable when function signature doesn't on a single line.

```kotlin
// Incorrect
fun longMethodName(
    argument: ArgumentType = defaultValue,
    anotherArgument: AnotherArgumentType
) = argument.foo(anotherArgument)

// Correct
fun longMethodName(
    argument: ArgumentType = defaultValue,
    anotherArgument: AnotherArgumentType
): ReturnType {
    return argument.foo(anotherArgument)
}
```

For now it's not known whether function chains are allowed in expression functions. On the one hand it can be treated as multiline expression without wrapping, on the other hand it reduces readability.

```kotlin
// Example from BinaryVersion.kt in official Kotlin source code.
fun parseVersionArray(string: String): IntArray? =
    string.split(".")
        .map { part -> part.toIntOrNull() ?: return null }
        .toTypedArray().toIntArray()
```
