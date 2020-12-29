# Kotlin Constructor

## 생성자 정의

```java
// java
public class Example {
  public Example() {

  }
}
```


```kotlin
// kotlin
public clas Example{
  init {

  }
}
```

## 인자가 있는 생성자


```java
// java
public class Example {
  public Example(int a) {

  }
}
```


```kotlin
// kotlin
public clas Example(a: Int){
  init {

  }
}
```


## 생성자의 인자를 통해 내부 프로퍼티에 값 전달


```java
// java
public class Example {
  int a;
  int b;
  public Example(int a, int b) {
    this.a = a;
    this.b = b;
  }
}
```


```kotlin
// kotlin
class Example(val a: Int, val b: int){

}
```


## 추가 생성자 선언

```java
// java
public class Example {
  int a;
  int b;
  public Example(int a, int b) {
    this.a = a;
    this.b = b;
  }
  public Example(int a){
    this(a, 0);
  }
}
```


```kotlin
// kotlin
class Example(val a: Int, val b: int){
  constructor(a: Int) : this(a, 0)
}
```

## 주 생성자 가시성



```kotlin
// kotlin
class Example internal constructor(val a: Int, val b: int){
  private constructor(a: Int) : this(a, 0)

  //접근 제한자 지정 안 할 시 public
  constructor(): this(0, 0)
}
```
