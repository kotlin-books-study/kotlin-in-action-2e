# 3장 문제 - 도혁

> 진도 : 3장 (함수 정의와 호출)

## Q1.

`JvmOverloads` 어노테이션은 어떤 역할을 수행하는지 코드를 예시로 들어 설명해주세요.

- **현정 :**
<br>

코틀린에서 **디폴트 파라미터**를 사용하면 함수를 호출할 때 **일부 파라미터를 생략**할 수 있다.

```kotlin
fun greet(name: String, greeting: String = "안녕", loud: Boolean = false) {
    val message = if (loud) "$greeting, $name!!!" else "$greeting, $name"
    println(message)
}
```

```kotlin
greet("현정")                   // greeting, loud 둘 다 생략
greet("현정", "반가워")          // loud만 생략
greet("현정", "반가워", true)    // 생략 X
```

하지만 **자바에는 디폴트 파라미터 개념 자체가 없다.** <br>
그래서 자바가 위 함수를 호출하면 **항상 모든 인자를 다 넘겨야** 한다.

```java
// 자바에서
GreetKt.greet("현정");                    // ❌ 컴파일 에러
GreetKt.greet("현정", "반가워", false);    // ✅ 모든 인자를 다 작성
```

### `@JvmOverloads`의 역할

```kotlin
@JvmOverloads
fun greet(name: String, greeting: String = "안녕", loud: Boolean = false) { ... }
```

`@JvmOverloads`어노테이션을 붙이면 **컴파일러가 자바용 오버로드 메서드들을 자동으로 생성**해준다.<br>
(파라미터를 뒤에서부터 하나씩 뺀 버전들을 만들어줌)

```java
// 컴파일러가 자바용 메서드들 자동 생성
void greet(String name)
void greet(String name, String greeting)
void greet(String name, String greeting, boolean loud)
```

그래서 자바에서도 파라미터를 골라서 호출할 수 있게 된다.

```java
GreetKt.greet("현정");                    // ✅
GreetKt.greet("현정", "반가워");           // ✅
GreetKt.greet("현정", "반가워", true);     // ✅
```

> [!WARNING]
> 오버로드는 **뒤에서부터** 잘려나간다. `name`만 있는 버전, `name + greeting` 버전은 만들어지지만, `greeting`을 건너뛰고 `name`과 `loud`만 있는 버전은 **안 만들어진다.** 자바의 오버로딩에서는 **"중간만 건너뛰기"를 표현할 방법이 없기 때문**이다.

- **도혁 :**

## Q2.

Kotlin 은 자바와 다르게 클래스에 속하지 않은 최상위 함수와 프로퍼티가 선언 가능하다. 자바에서도 이 함수와 프로퍼티를 사용할 수 있는데, 어떻게 가능한지 설명해주세요.

- **현정 :**
<br>

### **코틀린 컴파일러가 최상위 선언을 담을 클래스를 자동으로 생성한다.**

JVM에는 **클래스 밖의 함수·필드**가 존재할 수 없다. 모든 메서드와 필드는 반드시 어떤 클래스 안에 있어야 한다.<br>
그런데 코틀린은 함수·프로퍼티를 파일 최상위에 선언 가능하다.

```kotlin
// Join.kt
package strings

fun joinToString(list: List<Int>): String { ... }

const val MAX_COUNT = 100
```

이게 가능한 이유는 **코틀린 컴파일러가 `파일명 + Kt` 규칙으로 클래스를 자동으로 생성**한 뒤, 그 안에 정적(static) 멤버로 넣어준다.<br>
(`Join.kt` → `JoinKt` 클래스)

그래서 자바에서는 이 자동 생성된 클래스에 접근하기 때문에 가능하다.

```java
import strings.JoinKt;

String result = JoinKt.joinToString(list);   // 정적 메서드처럼 호출
int max = JoinKt.MAX_COUNT;                 // 정적 필드처럼 접근
```

- **도혁 :**
