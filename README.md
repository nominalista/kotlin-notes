# Kotlin notes

## Code style

### Expression functions

Expression functions are great tool to shorten the code. 

```kotlin
fun foo(x: String) = x.length
```

In order to keep balance between readability and usability it is not allowed to use expression functions with wrapping. If an expression function's return grows to require wrapping, use a normal function body, a `return` declaration, and normal expression wrapping rules instead.

```kotlin
// Proper formating - no wrapping
fun foo(x: String) =
    veryLongFunctionNameThatDoesNotFitInOneLine(x.length)
    
// Incorrect formatting - parameters forced to wrap functin
fun foo(x: String) =
    veryLongFunctionNameThatDoesNotFitInOneLine(x.length,
        x.chars)
```
