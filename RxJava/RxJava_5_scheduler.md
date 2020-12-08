# RxJava

# 스케줄러

## 스케줄러란

- RxJava만 사용한다고 작업이 비동기로 이루어지는 것은 아님
- 스레드를 지정해주지 않는 경우 작업은 현재 스레드(main)에서 일어남
- 스케줄러는 RxJava 코드를 어느 스레드에서 실행할지 지정 가능
- subscribeOn과 observeOn을 사용하면 데이터 흐름이 발생하는 스레드와 구독자에게 데이터를 발행하는 스레드 분리 가능
- Rxjava는 특정 스케줄러를 사용하다가 다른 스케줄러로 변경하기 쉬움

## 스케줄러 종류

RxJava의 스케줄러는 Schedulers 클래스의 정적 팩토리 메소드로 생성


```java
public final class Schedulers {
    @NonNull
    static final Scheduler SINGLE;

    @NonNull
    static final Scheduler COMPUTATION;

    @NonNull
    static final Scheduler IO;

    @NonNull
    static final Scheduler TRAMPOLINE;

    @NonNull
    static final Scheduler NEW_THREAD;
  }
```

|스케줄러|이름|내용|
|-|-|-|
|싱글|Schedulers.newThread()|단일 스레드르 생성해 계속 재사용|
|계산|Schedulers.computation()|내부적으로 스레드 풀 생성, 스레드 개수=프로세서 개수|
|IO|Schedulers.io()|필요할때마다 스레드를 계속 생성|
|트램펄린|Schedulers.trampoline()|현재 스레드에 무한한 크기의 대기 큐 생성|
|뉴 스레드|Schedulers.single()|매번 새로운 스레드 생성|



- RxJava에서는 계산, IO, 트램펄린 세가지의 스케줄러 권장





## NEW_THREAD Thread Scheduler

- 새로운 스케줄러 생성
- 요청을 받을 때 마다 새로운 스레드 생성
- Schedulers.newThread()



## COMPUTATION Thread Scheduler

- CPU에 대응하는 계산용 스케줄러
- 일반적인 계산/연산 시 사용
- IO작업을 하지 않는 스케줄러
- 내부적으로 스레드 풀 생성
- 스레드 개수= 프로세서 개수
- Schedulers.computation()



## IO Thread Scheduler

- IO 작업을 하거나 네트워크 요청 처리 시 사용
- 계산 스케줄러와 다르게 필요할때마다 스레드를 계속 생성
- Schedulers.io()



## TRAMPOLINE Thread Scheduler

- 새로운 스레드를 생성하지 않고 현재 스레드에 무한한 크기의 대기큐 생성
- Schedulers.trampoline()




## Single Thread Scheduler

- RxJava 내부에서 단일 스레드를 별도로 생성해 처리
- 한번 생성된 스레드로 여러 구독작업 처리
- 비동기 처리를 지향한다면 이걸 쓸일은 거의 없음
- Schedulers.single()



## Thread pool을 직접 생성하여 전달

- java에는 Executor를 통해 스레드 풀을 직접 생성 가능
- 권장 방법은 아님

```java
String[] source = {"First", "Second", "Third"};
Executor executor = Executors.newFixedThreadPool(10);
Observable.fromArray(source)
        .subscribeOn(Schedulers.from(executor))
        .subscribe(System.out::println);
```

















.
