# 7장 문제 - 현정

> 진도 : 7장 (널이 될 수 있는 값)

## Q1. 스마트 캐스트

표시한 부분에서 컴파일 에러가 나는 이유는 무엇인가요?

```kotlin
class UserHolder {
    var user: String? = null

    fun printLength() {
        if (user != null) {
            println(user.length)   // 여기
        }
    }
}
```

- **현정 :**
- **도혁 :**

## Q2. 입력값 검증

```kotlin
fun validate(input: String?): String = when {
    input == null -> "null"
    input.isEmpty() -> "비어있음"
    input.isBlank() -> "공백만"
    else -> "OK: ${input.trim()}"
}

fun main() {
    println(validate(null))
    println(validate(""))
    println(validate("   "))
    println(validate(" 현정 "))
}
```

- **현정 :**
- **도혁 :**
