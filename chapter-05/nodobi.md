# 5장 문제 - 도혁

> 진도 : 5장 (람다를 사용한 프로그래밍)

## Q1. 람다 함수의 재사용성

아래 코드의 출력을 예측하고 그 이유에 대해서 같이 설명해주세요

```java
// Foo.java
 public class Foo() {
    public static Runnable something(Runnable r) { return r; }
 }
```

```kotlin
// main.kt

class Bar(val title: String) {
    fun a1() = Foo.something { println("a") }
    fun a2() = Foo.something { println("a") }
    fun b() = Foo.something { println(title) }
    fun c(arg: Int) = Foo.something { println(arg) }
    fun d() = Foo.something(object: Runnable {
        override fun run() = println("d")
    })
}

fun main() {
    val s = Bar("A")
    println(s.a1() === s.a1())
    println(s.a1() === s.a2())
    println(s.b() === s.b())
    println(s.c(1) === s.c(1))
    println(s.d() === s.d())
}
```

- **현정 :**
- **도혁 :**

## Q2. 수신 객체와 람다

아래 코드를 실행했을 때 컴파일 오류가 발생하는 위치의 번호를 작성하고 나머지 부분의 출력 결과를 설명해주세요.

```kotlin
val a = run { 1 + 2 } // (1)
val b = let { 1 + 2 } // (2)

class Recipe(val name: String) {
    val c = let { it.name } // (3)
    val d = let { name } // (4)
}

fun main() {
    val r = Recipe("recipe")

    println(a)
    println(b)
    println(r.c)
    println(r.d)
}
```


- **현정 :**
- **도혁 :**
