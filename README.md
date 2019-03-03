# Kotlin notes

## Naming

Name of the function, class, variable, etc. should be simple as possbile, but not simpler. Using long, descriptive names is definitely better than shorter ones that tells nothing about what it is doing. Code formatting in the IDE should not be an excuse for using incomprehensible name.

### "create" vs "make" vs "build"

"create" means that we are going to creating something new, something unique. "make" is often used in context of some ordinary tasks. Moreover, we can "make" something from other components, whilst sometimes we "create" objects from nothing. In contrary, "build" process takes time and uses many external components.

```kotlin
// "create" implies that created account will be unique
fun createAccount()

// "make" implies that new object will be made from already existing one
fun makeEmployee(record: EmployeeRecord)

// "build" implies that process contains many stages
fun buildHtmlPage()
```

## Code style

Official code style rules for Kotlin can be found [here](https://kotlinlang.org/docs/reference/coding-conventions.html).

> To configure the IntelliJ formatter according to this style guide, please install Kotlin plugin version 1.2.20 or newer, go to Settings | Editor | Code Style | Kotlin, click on "Set from…" link in the upper right corner, and select "Predefined style / Kotlin style guide" from the menu.

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

Normal function body is especially desirable when function signature doesn't fit on a single line.

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
// Part of BinaryVersion.kt from kotlin-core
fun parseVersionArray(string: String): IntArray? =
    string.split(".")
        .map { part -> part.toIntOrNull() ?: return null }
        .toTypedArray().toIntArray()
```
