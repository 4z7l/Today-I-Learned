# RxJava

1. Reactive Programming 이란
2. Observable
3. 연산자
4. 스케줄러
5. RxAndroid



# 1. Reactive Programming 이란



## Reactive Programming

- `Reactive Programming`은 데이터 흐름과 전달에 관한 프로그래밍 패러다임
- 명령형 imperative 프로그래밍 : 정해진 절차에 따라 순서대로 실행
- 리액티브 프로그래밍 : 데이터 흐름을 먼저 정의하고 데이터가 변경되었을 때 연관되는 함수나 수식이 업데이트
- 내가 어떤 기능을 직접 정해서 실행하는 것이 하는 시스템에 어떤 이벤트가 발생했을때 처리하는 것
- 기존 프로그래밍이 pull 방식()이라면, 리액티브는 push 방식
- pull 방식 : 사용하려는 곳에서 데이터를 직접 가져와서 사용
- push 방식 : 데이터에 변화가 생기면 변화가 발생한 곳에서 새로운 데이터를 사용하려는 곳에 전달
- 리액티브 프로그래밍은 주변 환경과 끊임없이 상호작용을 함, 다만 프로그램이 주도하는 것이 아닌 환경이 변하면 이벤트를 받아 동작함



## RxJava

- 2013년 2월 넷플릭스에서 처음 소개한 라이브러리
- 2016년 10월 RxJava2를 발표함



> ReactiveX is a library for composing asynchronous and event-based programs by using observable sequences.
>
> It extends **the observer pattern** to support sequences of data and/or events and adds operators that allow you to compose sequences together declaratively while abstracting away concerns about things like low-level threading, synchronization, thread-safety, concurrent data structures, and non-blocking I/O.

- ReactiveX는 관찰 가능한 시퀀스를 통해 비동기/이벤트 기반 프로그램을 구성하기 위한 라이브러리이다. 
- Observer Pattern을 확장한다. 
- 데이터나 이벤트의 시퀀스를 지원한다.
-  시퀀스를 조합할수 있는 연산자를 지원한다. 
- 스레드, 동기화, I/O 블락에 관한 우려를 줄인다.





## RxJava Sample

```java
import io.reactivex.rxjava3.core.Observable;

public class RxExample {
    public static void main(String[] args){
        Observable.just("hi")
                .subscribe(System.out::println);
    }
}
```

- `just` : 가장 단순한 Observable 선언 방식
- `subscribe` : Observable을 구독함, 구독자가 subscribe를 호출해야 데이터가 발행됨



## Marble Diagram

https://rxmarbles.com/

![img](http://reactivex.io/assets/operators/legend.png)



- 실선 : timelint
- 모형 : Observable에서 발행하는 데이터
- 세로줄(파이프) : 데이터 발행의 완료, 이후에는 데이터 발행 불가능
- 가운데 박스 : 함수(flip, map, ...)
- x : 에러 발생