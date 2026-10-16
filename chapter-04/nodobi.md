# 4장 문제 - 도혁

> 진도 : 4장 (클래스, 객체, 인터페이스)
## Q1. 커스텀 접근자와 가시성 변경자

```kotlin
interface Counter {
    var count: Int
        get() = field // (1)

    val isEven: Boolean
        get() = count % 2 == 0 // (2)

    fun increase()
}

open class BasicCounter(): Counter {
    override var count: Int = 0
        private set // (3)

    final override fun increase() { // (4)
        count++

        println(count)
        println(isEven)
    }
}
```

위 코드에서 컴파일 에러가 발생하는 부분의 번호와 그 이유에 대해서 설명해주세요

- **현정 :**
- **도혁**

정답은 (1), (3)

### (1) Interface의 프로퍼티는 `Backing field` 를 가질 수 없다.

[코틀린 컴파일러는 프로퍼티의 값이 메모리에 저장되어야 할 때 `Backing Field`를 생성한다.](https://kotlinlang.org/docs/properties.html#backing-fields)

예를 들어 이 코틀린 파일이 자바 코드로 변환된다면 아래처럼 변환된다.
```kotlin

// .kt file
val foo: String = ""
    get() = {
        "Custom getter of $field"
    }

```

```java
// .java file
@NotNull
private String foo = "";

@NotNull
public final String getFoo() { return "Custom getter of " + this.foo; }
```

프로퍼티의 커스텀 게터에서 `field` 키워드를 사용했으므로, 사용할 때 마다 저장된 값을 참조하여 게터 블럭을 실행해야 한다.
이 때 값을 저장하기 위한 `foo` 필드가 `Backing Field` 이다.
 
그 이유는 자바와의 상호 운용성을 생각해보면 쉽게 이해할 수 있다.
자바와의 상호코틀린의 인터페이스도 자바의 인터페이스로 변환이 되어야 하므로 상태를 저장하기 위해 필드를 사용할 수 없다.
따라서 내부적으로 필드(`Backing Field`)를 생성하는 구문은 코틀린의 인터페이스에서도 사용할 수 없다.

### (3). 오버라이드는 가시성을 좁힐 수 없다.

Counter 에서 별도의 가시성 변경자를 사용하지 않았으므로, public 으로 선언된다.

따라서 Counter 의 setter 를 private 혹은 protected 같이 가시성이 좁아지는 변경자를 붙일 수 없다.

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

// Main.java
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

정답은 (1), (4)

### object 객체는 내부에서, companion object 는 속한 클래스에서 객체를 가진다.

object 객체는 내부적으로 INSTANCE 라는 필드로 객체를 관리한다. 
즉, NormalObject 를 자바 코드로 변환해서 보면, 아래처럼 변환된다.

```java
public static final class NormalObject {
    public static final NormalObject INSTANCE = new NormalObject();

    // ..
}
```

이와 다르게, Companion object 는 속한 클래스에서 명시한 이름과 동일한 필드로 객체를 관리한다.
따라서 CompanionObject 를 자바 코드로 변환해서 보면, 아래처럼 변환된다.

```java
public class Foo() {
    public static final CompanionObject CompanionObject = new CompanionObject();
}
```

따라서 (1) 의 경우엔, `Foo.NormalObject` 가 의마하는 것이 클래스 이름이므로 함수를 호출하지 못하는 것이고,
(2) 는 `Foo.CompanionObject` 가 Foo 클래스의 CompanionObject 필드를 지칭하는 것이기 때문에 컴파일 에러가 발생한다.

반대로 (3) 의 경우엔, `Foo.NormalObject.INSTANCE` 가 NormalObject 의 INSTANCE 필드를 지칭하는 것이기 때문에 호출 가능하며 (4) 는 `INSTANCE` 라는 필드가 `Foo.CompanionObject` 클래스 내부에 없으므로 컴파일 에러가 발생한다.


### JvmStatic

`JvmStatic` 은 붙은 메소드의 Jvm 용 static 메소드를 생성해주는 만들어주는 어노테이션이다.
object 클래스의 메소드에 붙이는 경우, `final static` 메소드로 변환되기 때문에, 아래처럼 변환되고 클래스 이름으로 접근이 가능하고 아래 코드에서 컴파일 에러가 발생하지 않는다.

```java
public class Foo {
    
    public static final class NormalObject {
        
        // ...

        @JvmStatic
        public static final void staticBar() {
            System.out.println("annotated Companion");
        }
    }
}

// static 메소드를 호출하는 것이기 때문에 컴파일 에러가 발생하지 않음
Foo.NormalObject.staticBar();

```

만약 이 어노테이션을 companion object 객체의 메소드에 사용하는 경우엔 조금 다르게 작동한다. `static final` 메소드로 변환하는 것은 동일하지만 이걸 호출하는 메소드를 외부 클래스에도 동일하게 선언한다.


```java
public class Foo {
    public static final CompanionObject CompanionObject = new CompanionObject();

    @JvmStatic
    public static final void staticBar() { CompanionObject.staticBar(); }

    // .. 

    public static final class CompanionObject {
        
        // ...

        @JvmStatic
        public sattic final void staticBar() {
            System.out.println("annotated Companion");
        }
    }
}

// 두 메소드는 동일한 동작을 수행
Foo.staticBar();
Foo.CompanionObject.staticBar();
```