# Kotlin Delegates

- 다른 object에게 task를 위임할 수 있음 --> 코드 재사용 증가

- Kotlin에서는 Delegates를 `by` 키워드를 통해 제공함

- built-in delegates들도 있음 : `lazy()`, `observable()`, `vetoable()`, `notNull()`


<br>

## lazy()

- 속성이 처음 사용될때 초기화되도록 함
- 생성될 때 많은 비용이 소모된다면 아주 도움이 될 것임 (아직 attach되지않은 fragment의 변수에서 context를 필요로할때 lazy를 사용하는 거인듯..)
- `LazyThreadSafeMode` : 초기화를 다른 스레드에서 시킬 것인지 결정가능, default = `LazyThreadSafetyMode.SYNCHRONIZED`
- lambda : 처음 초기화될때 접근하며, 이후 저장될 값 지정

```kotlin
val name: String by lazy() {
    "hi"
}
```



<br>

## Delegates.observable()

- Observer 패턴을 이용
- 두가지 parameter : 초기값과 상태가 변경되었을때 호출될 listener
- `setValue()` 다음에 `ObservableProperty.afterChange()`가 호출됨
- `beforChange()`도 있지만 사용되지 않음, 단 `vetoable()`의 base가 됨

```kotlin
var address: String by Delegates.observable("not entered yet"){ _, _, _ ->
    // update when value changed
}
```



<br>

## Delegates.notNull()

- 나중에 초기화를 시켜줌
- 보통은 `lateinit`을 쓰지만, `lateinit`이 지원해주지 않는 primitive type에 대해 `notNull()`을 쓸 수 있다. 

```kotlin
val name: String by Delegates.notNull<String>()
```



<br>

## Vetoable()

- 변경권 거부 가능(??)
- lambda가 true 반환 시 value는 수정됨, false 반환 시 그대로

```kotlin
var address: String by Delegates.vetoable(""){ _, _, _ ->
    // something
}
```





<br><br>

> :bookmark: **REFERENCE**
>
> https://medium.com/androiddevelopers/built-in-delegates-4811947e781f
