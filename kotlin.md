# Kotlin

- [2-1. 기본 자료형과 변수 선언 방법](#2-1-기본-자료형과-변수-선언-방법)
- [2-2. 나를 괴롭히는 Null](#2-2-나를-괴롭히는-null)
- [2-3. 검사와 자료형을 변환해보기](#2-3-검사와-자료형을-변환해보기)
- [3-1. 함수를 선언하고 호출해보기](#3-1-함수를-선언하고-호출해보기)
- 3-2 함수를 활용한 예제 만들기
- [3-3.  함수형 프로그래밍 패러다임!](#3-3--함수형-프로그래밍-패러다임)
- [4-1. 이름없는 함수의 또 다른 형태, 람다(Lambda)!](#4-1-이름없는-함수의-또-다른-형태-람다lambda)
- [4-2 고차함수와 람다식의 이해](#4-2-고차함수와-람다식의-이해)
- [4-3 다양한 함수의 출격](#4-3-다양한-함수의-출격)
- [4-4 함수와 변수의 범위(Scope)](#4-4-함수와-변수의-범위scope)
- 5-1 조건문을 통한 분기
- [5-2 반복문으로 여러번!](#5-2-반복문으로-여러번)
- [5-3 흐름의 중단과 반환](#5-3-흐름의-중단과-반환)
- [5-4 예외가 발생했어요!](#5-4-예외가-발생했어요)
- [6-1 준비운동! 람다식과 고차함수 요약](#6-1-준비운동-람다식과-고차함수-요약
)
- [6-2 널 포획해야겠어! 클로저(Closure)](#6-2-널-포획해야겠어-클로저closure
)
- [6-3 너 한일은 결과와 함께 반환해. 알았지? - let()](#6-3-너-한일은-결과와-함께-반환해-알았지---let
)
- [6-4 너 할일해. 난 그냥 반환할께. 올쏘! - also()](#6-4-너-할일해-난-그냥-반환할께-올쏘---also
)
- [6-5 널 확장 시켜놓고 난 반환한다. - apply()](#6-5-널-확장-시켜놓고-난-반환한다---apply
)
- [6-6 그냥 실행하고 결과를 반환 - run()](#6-6-그냥-실행하고-결과를-반환---run
)
- [6-7 난 단독으로 실행되 반환하는 녀석이지 - with()](#6-7-난-단독으로-실행돼-반환하는-녀석이지---with
)
- [6-8 사용했으면 닫어! 쫌! - use()](#6-8-사용했으면-닫어-쫌---use)
- 6-9 자주 사용되는 기타 표준 함수 (람다식검사, 시간측정, 난수 생성)



<br>

> :bookmark: [[부스트코스] 코틀린 프로그래밍 기본1/2(함수편)](https://www.edwith.org/boostcourse-mo-kotlin-basic1/home)


<br>

## 2-1. 기본 자료형과 변수 선언 방법

### 변수
`val` : 불변형 (value, immutable) <br>
`var` : 가변형 (variable, mutable)

`val 변수이름 : 타입 = 값`

### 자료형
- 기본형 (Primitive) : 순수 자료형, (int, long, ...)
- 참조형 (Reference) : 객체가 됨, 동적 공간에 데이터를 두고 참조함 (Int, Long, Float, Double)

### 문자열
- String으로 선언
- String Pool 이라는 공간에 구성됨
- $ 기호로 문자열 출력 가능
```kotlin
var a = 1
val str = "a is ${a+2}"
```

<br>

## 2-2. 나를 괴롭히는 Null

__Kotlin의 변수 선언은 기본적으로 NotNull__

- `?` : null 이 가능하다고 알려줌
ex) `val a : Int? = null`

- `?.` : 변수가 null이면 뒷부분 실행 안함
```kotlin
var str : String?
str = null
println("length : ${str?.length}")
// 출력 결과 : length : null
``` 
- `!!` : null일리 없다!! 웬만하면 사용하지 말자

### Elvis Operator
- null 확인 방법
`val l: Int = if (b != null) b.length else -1`
- Elvis Operator
`val l = b?.length ?: -1`

<br>

## 2-3. 검사와 자료형을 변환해보기

### `==` 와  `===`

`==` : 값만 비교<br>
`===` : 값과 참조주소 비교<br>

```kotlin
val a: Int = 128
val b : Int = 128
println(a==b) //true
println(a===b) //true
```

```kotlin
val a: Int = 128
val b : Int? = 128
println(a==b) //true
println(a===b) //true
```

> __Java__에서 `==` 는 값과 참조주소를 모두 비교함

### is

```kotlin
// 변수가 특정 자료형인지 아닌지 확인
if (num is Int) println(num)
else if (num !is Int) println("not a Int)
```

### Any
- 모든 클래스의 뿌리
- 자료형이 정해지지 않은 경우


<br>

## 3-1. 함수를 선언하고 호출해보기

### 함수

__함수 정의 방법__

```kotlin
fun 함수 이름([변수 이름: 자료형, 변수 이름: 자료형..]  ): [반환값의 자료형] { 
    표현식...
    [return 반환값] 
}
```

```kotlin
fun sum(a: Int, b: Int) : Int {
	var sum = a + b
	return sum
}
```

__간략화 할 경우__
```kotlin
fun sum(a: Int, b: Int) = a + b
```

### 매개변수 기본값 지정 가능
```kotlin
fun add(name: String, email: String = "default") {
  // name과 email을 회원 목록에 저장
} 
...
add("Youngdeok") // email 인자를 생략하여 호출(name에만 "Youngdeok"이 전달됨)
```

### 매개변수 이름과 함께 호출 가능
```kotlin
fun namedParam(x: Int = 100, y: Int = 200, z: Int) {
    println(x + y + z)
}

...
namedParam(x = 200, z = 100) // x, z의 이름과 함께 함수 호출(y는 기본값 사용)
```

### 가변인자를 가진 함수
인자의 개수가 변할 수 있는 함수 -> `vararg` (variable argument) 사용
```kotlin
fun main(args: Array<String>) {

    normalVarargs(1, 2, 3, 4) // 4개의 인자 구성
    normalVarargs(4, 5, 6)    // 3개의 인자 구성
}

fun normalVarargs(vararg counts: Int) {
    for (num in counts) {
        println("$num")
    }
    print("\n")
}
```

<br>

## 3-3.  함수형 프로그래밍 패러다임!

### 코틀린은 다중 패러다임 언어
- __함수형 프로그래밍__
	+ 코드 간략, 테스트나 재사용성 증가
	+ 람다식, 고차 함수, 순수 함수
	+ 모듈화 하므로 디버깅, 테스트 용어
	+ 생산성 높음

### 순수 함수
- side-effect 없는 함수 : __입력이 같으면 항상 출력이 같다!!__
- 입력과 내용을 분리하고 모듈화함
- 함수의 값을 예측할 수 있어 테스트, 디버깅 용이

### 람다식
- 익명 함수의 한 형태
- 람다 대수 (Lambda calculus)로 부터 유래

### 일급 객체(First Class Citizen)
- 함수의 인자로 전달 가능
- 함수의 반환값에 사용 가능
- 변수에 담을 수 있음
__--> 코틀린의 함수는 일급 객체임__

### 고차 함수(high-order function)
```kotlin
fun main() {
    println(highFunc({ x, y -> x + y }, 10, 20)) // 람다식 함수를 인자로 넘김
}

fun highFunc(sum: (Int, Int) -> Int, a: Int, b: Int): Int = sum(a, b) // sum 매개변수는 함수  
```

<br>

## 4-1. 이름없는 함수의 또 다른 형태, 람다(Lambda)!

### 람다식 선언과 할당
```kotlin
fun main() {

    var result: Int

    // 일반 변수에 람다식 할당
    val multi = {x: Int, y: Int -> x * y}
    // 람다식이 할당된 변수는 함수처럼 사용 가능
    result = multi(10, 20)
    println(result)
}
```

```kotlin
val multi: (Int, Int) -> Int = {x: Int, y: Int -> x * y} // 생략되지 않은 전체 표현
val multi = {x: Int, y: Int -> x * y}  // 선언 자료형 생략
val multi: (Int, Int) -> Int = {x, y -> x * y} // 람다식 매개변수 자료형의 생략
```


### 반환 자료형 없거나 매개변수 하나일때
```kotlin
val greet: ()->Unit = { println("Hello World!") }
val square: (Int)->Int = { x -> x * x }
```

### 선언부 자료형 생략
```kotlin
val greet = { println("Hello World!") }
val square = { x : Int -> x * x }

val nestedLambda1 : ()->()->Unit = { { println("nested") } }
val nestedLambda2 = { { println("nested") } }

```

<br>

## 4-2 고차함수와 람다식의 이해

### Call by Value

- 함수가 인자로 전달될 경우 람다식 함수는 값으로 처리됨
```kotlin
fun main() {
    val result = callByValue(lambda()) // 람다식 함수를 호출
    println(result)
}

fun callByValue(b: Boolean): Boolean { // 일반 변수 자료형으로 선언된 매개변수
    println("callByValue function")
    return b
}

val lambda: () -> Boolean = {  // 람다 표현식이 두 줄이다
    println("lambda function")
    true 		    // 마지막 표현식 문장의 결과가 반환
}
```

- 람다식 이름만 사용
```kotlin
fun main() {
    val result = callByName(otherLambda) // 람다식 이름으로 호출
    println(result)
}

fun callByName(b: () -> Boolean): Boolean { // 람다식 함수 자료형으로 선언된 매개변수
    println("callByName function")
    return b()
}

val otherLambda: () -> Boolean = {
    println("otherLambda function")
    true
}
```

<br>

## 4-3 다양한 함수의 출격

### 익명 함수
- 함수가 이름이 없는 것
- return, break, continue 사용하기 어려움(의도한 대로 안돼서)
```kotlin
fun(x: Int, y: Int): Int = x + y // 함수 이름이 생략된 익명 함수
```

### 인라인 함수
- 함수의 분기 없이 처리 -> 성능 증가
- 내용이 많은 함수에 사용하면 안됨!
- `inline` 키워드 사용
- `noinline` : 람다식 함수가 inline 되는 것을 막음
```kotlin
fun main() {
	...
	sub()
	sub()
	...
}
inline fun sub() {
	...
}
```


### 확장 함수
- 클래스의 멤버 함수를 외부에서 더 추가 가능
- 기존의 표준 라이브러리를 수정하지 않고도 확장 가능
```kotlin
fun 확장대상.함수명(매개변수) : 반환값 {
	return 값
}
```

```kotlin
fun main() {
    val source = "Hello World!"
    val target = "Kotlin"
    println(source.getLongString(target))
}

// String을 확장해 getLongString 추가
fun String.getLongString(target: String): String =
        if (this.length > target.length) this  else target
```

### 중위 함수
- `infix` 키워드 사용
- 직관적임 
- 비트 연산자에서 주로 사용함

```kotlin
...
    // 중위 표현법
    val multi = 3 multiply 10
...

// Int를 확장해서 multiply() 함수가 하나 더 추가되었음
infix fun Int.multiply(x: Int): Int {  // infix로 선언되므로 중위 함수
    return this * x
}
```

### 꼬리 재귀 함수
- 분기가 없음
- stack overflow 방지
- `tailrec` 키워드 사용

- 일반 재귀 함수
```kotlin
fun main() {
	val number = 5
    println("Factorial: $number -> ${factorial(number)}")
}

fun factorial(n: Int) : Long {
	return if (n==1) n.toLong() else n*factorial(n-1)
}

```

- 꼬리 재귀 함수
```kotlin
fun main() {
    val number = 5
    println("Factorial: $number -> ${factorial(number)}")
}

tailrec fun factorial(n: Int, run: Int = 1): Long {
    return if (n == 1) run.toLong() else factorial(n-1, run*n)
}
```

<br>

## 4-4 함수와 변수의 범위(Scope)

### 전역 변수
- 최상위에 있는 변수
- 프로그램이 실행되는 동안 삭제되지 않고 메모리에 유지됨
- 자주 사용되지 않는 전역 변수는 메모리 자원 낭비

### 지역 변수
- 특정 코드 블록 내에서만 사용
- 스택 메모리 사용


<br>

## 5-1 조건문을 통한 분기

### 범위 연산자
- `변수명 in 시작값..마지막값`
- `if(score>=80 && score<=89.9)` -> `score in 80..89.9`  로 바꾸기 가능!

### when
- `break` 사용하지 않아도 됨
```kotlin
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> { // 블록 구문 사용 가능
        print("x는 1, 2가 아닙니다.")
    }
}
```

- `in`과 `is` 키워드 사용 가능
```kotlin
when (x) {
	in 1..10 -> println("1이상 10이하")
	!in 10..20 -> println("10이상 20이하에 포함되지 않음")
	else -> println("")
}
```

```kotlin
val result = when(str) {
	is String -> "문자열입니다"
}
```


<br>

## 5-2 반복문으로 여러번!

### for
- 하행 반복 : `for (i in 5 downTo 1) print(i)`
- 필요한 단계 증가 : `for(i in 1..5 step 2) print(i)`
- 혼합 사용 : `for (i in 5 downTo 1 step 2) print(i)`


<br>

## 5-3 흐름의 중단과 반환

### 람다식에서 라벨을 이용한 return

```kotlin
fun inlineLambda(a: Int, b: Int, out: (Int, Int) -> Unit) { // inline이 제거됨
    out(a, b)
}

fun retFunc() {
    println("start of retFunc")
    inlineLambda(13, 3) lit@{ a, b ->  // ① 람다식 블록의 시작 부분에 라벨을 지정함
        val result = a + b
        if(result > 10) return@lit // ② 라벨을 사용한 블록의 끝부분으로 반환
        println("result: $result")
    } // ③ 이 부분으로 빠져나간다
    println("end of retFunc") //  ④ 이 부분이 실행됨 
}
```

<br>

## 5-4 예외가 발생했어요!

```kotlin
try {
    예외 발생 가능성 있는 문장
} catch (e: 예외처리 클래스명) {
    예외를 처리하기 위한 문장
} finally {
   반드시 실행되어야 하는 문장
}
```

<br>

## 6-1 준비운동! 람다식과 고차함수 요약
```kotlin
fun inc(x: Int): Int {
    return x + 1
}

fun high(name: String, body: (Int)->Int): Int {
    println("name: $name")
    val x = 0
    return body(x)
}
```

```kotlin
// 함수를 이용한 람다식
val result = high("Sean", {  x -> inc(x + 3) })

// 소괄호 바깥으로 빼내고 생략
val result2 = high("Sean") { inc(it + 3) }

// 매개변수 없이 함수의 이름만 사용할 때
val result3 = high("Kim", ::inc)

// 람다식 자체를 넘겨 준 형태
val result4 = high("Sean") { x -> x + 3 }

// 매개변수가 한 개인 경우 생략
val result5 = high("Sean") { it + 3 }
```

<br>

## 6-2 널 포획해야겠어! 클로저(Closure)

### Closure
- 람다식으로 표현된 내부 함수에서 외부 범위에 선언된 변수에 접근할 수 있는 개념
- 람다식 안에 있는 외부 변수는 람다가 capture(포획)한 변수

```kotlin
fun main() {

    val calc = Calc()
    var result = 0 // 외부의 변수
    calc.addNum(2,3) { x, y -> result = x + y }  // 클로저
    println(result) // 값을 유지하여 5가 출력
}

class Calc {
    fun addNum(a: Int, b: Int, add: (Int, Int) -> Unit) { // 람다식 add에는 반환값이 없음
        add(a, b)
    }
}
```

<br>

## 6-3 너 한일은 결과와 함께 반환해. 알았지? - let()

### 코틀린 제공 표준 라이브러리 함수
- `let()`, `apply()`, `with()`, `also()`, `run()`

|함수명|람다식 접근 방법|반환 방법|
|:--:|:--:|:--:|
|T.let|it|block 결과|
|T.also|it|T caller(it)|
|T.apply|this|T caller(this)|
|T.run / run|this|block 결과|
|with|this|Unit|


```kotlin
public inline fun <T, R> T.let(block: (T) -> R): R { ... return block(this) }

public inline fun <T> T.also(block: (T) -> Unit): T { block(this); return this }

public inline fun <T> T.apply(block: T.() -> Unit): T { block(); return this }

public inline fun <R> run(block: () -> R): R  = return block()
public inline fun <T, R> T.run(block: T.() -> R): R = return block()

public inline fun <T, R> with(receiver: T, block: T.() -> R): R  = receiver.block()

public inline fun <T : Closeable?, R> T.use(block: (T) -> R): R 

```


### let()
- inline 함수
- 함수를 호출하는 객체를 다음에 오는 block의 인자로 넘기고 특정 결과값을 반환
- 다른 메소드를 실행하거나 연산을 수행해야 하는 경우 사용

<br>

- let을 사용해 null 검사 대체 가능
```kotlin
    val score: Int? = 32
...
    // let을 사용해 null 검사를 제거
    fun checkScoreLet() {
        score?.let { println("Score: $it") } // ①
        val str = score.let { it.toString() } // ②
        println(str)
    }
```

<br>

- chaining
```kotlin
var a = 1
var b = 2

a = a.let { it + 2 }.let {
    val i = it + b
    i  // 마지막 식 반환
}
```

<br>

## 6-4 너 할일해. 난 그냥 반환할께. 올쏘! - also()

### also()
- also()를 호출하는 객체 T를 다음에오는 block에 전달하고 객체 T 자체를 반환

```kotlin
var m = 1
m = m.also { it + 3 }
println(m) // 출력 : 1
```


### let()과 also() 차이

- let()
```kotlin
val person = Person("Kildong", "Kotlin")

val a = person.let {
	it.skills = "Java"
	"Success"
}

println("a is $a")	// "a is Success"
println("person is $person") // "person is Person(name=Kildong, skills=Java)"
```

- also()
```kotlin
val person = Person("Kildong", "Kotlin")

val a = person.also {
	it.skills = "Java"
	"Success"
}

println("a is $a")	// "a is Person(name=Kildong, skills=Java)"
println("person is $person") // "person is Person(name=Kildong, skills=Java)"
```

<br>

## 6-5 널 확장 시켜놓고 난 반환한다. - apply()

### apply()
- also()와 비슷
- apply()를 호출한 객체 T를 다음에 오는 block에 전달하고 객체 자체 this를 반환

```kotlin
var person = Person("Kildong", "Kotlin")

    person.apply { this.skills = "Swift" }
    println(person)	// 출력 : "Person(name=Kildong, skills=Swift)

    val retrunObj = person.apply { 
        name = "Sean"
        skills = "Java"
    }
    println(person)	// 출력 : "Person(name=Sean, skills=Java)
    println(retrunObj)	// 출력 : "Person(name=Sean, skills=Java)
```

<br>

## 6-6 그냥 실행하고 결과를 반환 - run()

### run()
- 두 가지 형태 존재
- 익명 함수처럼 단독 사용 or 확장 함수처럼 호출

### apply()와 run() 비교

```kotlin
var person = Person("Kildong", "Kotlin")

val returnObj1 = person.apply{
	this.name = "Sean"
	this.skills = "Java"
	"Success"
}
println(person)						// 출력 : "Person(name=Seam, skills=Java)"
prinln("returnObj1 : $returnObj1")	// 출력 : "returnObj1 : Person(name=Seam, skills=Java)"

val returnObj2 = person.run {
	this.name = "Dooly"
	this.skills = "C#"
	"Success"
}
println(person)					// 출력 : "Success"
println("returnObj2 : $returnObj2")	// 출력 : "returnObj2 : Person(name=Dooly, skills=C#)"

```

<br>

## 6-7 난 단독으로 실행돼 반환하는 녀석이지 - with()

### with()
- 인자로 받는 객체를 다음에 오는 block의 receiver로 전달하여 결과값 반환
- `run()`의 경우 receiver가 없지만 `with()`는 receiver가 있음

```kotlin
val user = User("Kildong", "default")

val result = with (user) {
	skills = "Kotlin"
	email = "kildong@example.com"
}
println(user)		//출력 : "User(name=Kildong, skills=Kotlin, email=kildong@example.com)
println("result : $result")		//출력 : result : kotlin.Unit

```

<br>

## 6-8 사용했으면 닫어! 쫌! - use()

### use()
- 객체를 사용한 후 닫아야 하는 경우 -> `use()`를 사용하면 `close()`를 자동으로 호출해 닫아줌

```kotlin
fun main() {

    PrintWriter(FileOutputStream("d:\\test\\output.txt")).use {
        it.println("hello")
    }
}
```


