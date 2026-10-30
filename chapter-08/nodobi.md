# 8장 문제 - 도혁

> 진도 : 8장 (기본 타입, 컬렉션, 배열)

## Q1. Immutable, Persistent

이 소스코드를 실행하면 출력되는 메세지를 작성해주세요.

```kotlin
fun main() {
    val mutableList = mutableListOf("김치")
    val list: List<String> = mutableList
    mutableList.add("두부")

    val persistent = persistentListOf("김치")
    val immutable: ImmutableList<String> = persistent
    val added = persistent.adding("두부")

    println(list)
    println(immutable)
    println(added)
}
```

- **현정 :**
- **도혁 :**