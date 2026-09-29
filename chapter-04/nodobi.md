# 4장 문제 - 도혁

> 진도 : 4장 (클래스, 객체, 인터페이스)
## Q1. 커스텀 접근자와 가시성 변경자

```kotlin
interface Counter {
    var count: Int
        get() = field

    val isEven: Boolean
        get() = count % 2 == 0

    fun increase()
}

open class BasicCounter(): Counter {
    override var count: Int = 0
        private set

    final override fun increase() {
        count++

        println(count)
        println(isEven)
    }
}
```

위 코드에서 컴파일 에러가 발생하는 부분과 그 이유에 대해서 설명해주세요

- **현정 :**
- **도혁 :**

## Q2. object vs companion object

```kotlin

// Foo.kt
class Foo {
    object NormalObject {
        fun bar() {
            println("Normal")
        }

        @JvmStatic
        fun staticBar() {
            println("annotated Companion")
        }
    }

    companion object {
        fun bar() {
            println("Companion")
        }

        @JvmStatic
        fun staticBar() {
            println("annotated Companion")
        }
    }
}

```

```Java
public class Main {

    public static void main(String[] args) {
        Foo.NormalObject.bar(); // (1)
        Foo.CompanionObject.bar(); // (2)

        Foo.NormalObject.INSTANCE.bar(); // (3)
        Foo.CompanionObject.INSTANCE.bar(); // (4)

        Foo.NormalObject.staticBar(); // (5)
        Foo.CompanionObject.staticBar(); // (6)

        Foo.staticBar(); // (7)
    }
}
```

이러한 코드가 작성되었을 때 (1) ~ (7) 중 컴파일 에러가 발생하는 라인과 그 이유를 설명해주세요.


- **현정 :**
- **도혁 :**