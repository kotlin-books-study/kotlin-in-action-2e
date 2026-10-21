# 7장 문제 - 도혁

> 진도 : 7장 (널이 될 수 있는 값)

## Q1. 플랫폼 타입

아래 코드에서 플랫폼 타입이 설명되는 부분의 숫자를 작성하고, 그 이유를 설명해주세요

```java
import org.jetbrains.annotations.NotNull;
import org.jetbrains.annotations.Nullable;

public class User {
    public String nickname;
    public String getName() { return "kim"; }
    public String getNullName() { return null; }
    public int getAge() { return 20; }
    @Nullable public String getEmail() { return null; }
    @NotNull public String getId() { return "1"; }
}
```

```kotlin
val user = User() // (1)
val nickname = user.nickname // (2)
val name = user.name // (3)
val nullName = user.nullName // (4)
val age = user.age // (5)
val email = user.email // (6)
val id = user.id // (7)
```

- **현정 :**
- **도혁 :**