# 3장 문제 - 현정

> 진도 : 3장 (함수 정의와 호출)

## Q1. 확장 함수 출력 예측

```kotlin
open class Animal
class Dog : Animal()

fun Animal.sound() = "Some sound"
fun Dog.sound() = "Woof"

fun main() {
    val a: Animal = Dog()
    val d: Dog = Dog()
    println(a.sound())
    println(d.sound())
}
```

- **현정 :**
- **도혁 :**

## Q2. 출력 예측

```kotlin
class Logger {
    fun log(message: String, tag: String = "APP") = "[$tag] $message"
}

fun Logger.log(message: String, tag: String = "EXT") = "<$tag> $message"

fun main() {
    val logger = Logger()
    println(logger.log("start"))
    println(logger.log("error", tag = "NET"))
}
```

- **현정 :**
- **도혁 :**
