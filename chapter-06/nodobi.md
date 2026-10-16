# 6장 문제 - 도혁

> 진도 : 6장 (컬렉션과 시퀀스)

## Q1. 비어있는 컬렉션의 연산

아래 코드의 실행 결과를 작성하세요

```kotlin
val emptyList = emptyList<Int>()
val list = listOf(1, 2, 3)

println(emptyList.all { it > 42 })
println(emptyList.any { it > 42 })
println(emptyList.none { it > 42 })
println(emptyList.none())
println(list.filter { it > 42 }.all { it > 42 })
```

- **현정 :**
- **도혁 :**

## Q2. 시퀀스의 재사용성

아래 코드의 실행 결과를 작성하고 그 이유를 설명해주세요

```kotlin
var n = 0
val seqWithSeed = generateSequence(0) { if(it < 3) it + 1 else null}
val seq = generateSequence {  if(n <= 3) n++ else null }

println(seqWithSeed.toList())
println(seqWithSeed.toList())
println(seq.toList())
println(seq.toList())
```

- **현정 :**
- **도혁 :**