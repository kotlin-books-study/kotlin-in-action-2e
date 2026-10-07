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

### 확장 함수는 변수 타입에 따라 호출된다

`a` 는 `Dog` 인스턴스로 생성되었지만 변수 타입이 `Animal` 이다. 따라서 변수 타입에 맞는 `fun Animal.sound()` 확장함수가 호출된다.

`b` 도 마찬가지로 변수 타입이 `Dog` 이므로, 타입에 맞는 `fun Dog.sound()` 확장함수가 호출된다.

```
Some sound
woof
```

### 타입 캐스팅

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

### 멤버 함수는 확장 함수보다 우선순위가 높다.

멤버 함수와 확장 함수가 동일한 함수 시그니처를 가진다면, 멤버 함수가 항상 우선순위를 가진다
따라서 출력 결과는 아래와 같다.

```
[APP] start
[NET] error
```

**왜 이렇게 설계했을까?**

이렇게 설계한 이유에 대해서 추측을 해보자면, 외부 SDK 에서 선언된 함수를 사용자가 마음대로 확장 함수로 덮어버릴 수 있기 때문이지 않을까 추측해본다.
외부 함수의 클래스의 핵심 메소드를 사용자가 마음대로 변경할 수 있다면, 그로 인해 어떠한 변화가 일어날지 예측할 수 없고, 그렇기 때문에 제한해둔 부분이라고 생각했다.