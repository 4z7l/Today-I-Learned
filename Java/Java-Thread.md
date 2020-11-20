# JAVA Thread

## Thread란?

- Thread는 실행 단위
- JVM에 의해 스케줄되는 실행 단위 코드 블록
- `프로세스` : 같은 응용프로그램이어도 프로세스별로 고유한 메모리 영역을 보유, context switch에 비용 큼
- `스레드` : 같은 응용프로그램이면 자원과 메모리 공유, context switch에 따른 비용 적음

<br>

## JVM와 스레드

- 하나의 JVM은 한 번에 하나의 응용프로그램만 실행 가능
- 단, 하나의 응용프로그램에서 여러개의 스레드 생성 가능
- 스레드 생성 -> TCB(Thread Control Block : 스레드 코드 시작 주소, 스레드 상태, 우선순위 등 스레드에 대한 정보를 담음) 생성 -> JVM이 TCB 관리, JVM이 스레드 스케줄링 담당


## TCB(Thread Control Block)

|field|type|value|
|-|-|-|
|이름|String|스레드의 이름, 사용자가 지정|
|ID|정수|스레드 고유 ID|
|Program Counter|정수|현재 실행 중인 스레드 코드 주소|
|상태|정수|`NEW`,`RUNNABLE`,`WAITING`,`TIMED_WAITING`,`BLOCK`,`TERMINATED`|
|우선순위|정수|우선순위 값(1~10), 10이 젤 높음|
|그룹|정수|여러개의 스레드가 하나의 그룹을 형성할 수 있음, 속한 그룹의 정보|
|레지스터 스택|메모리 블록|스레드가 실행되는 도안 레지스터 값|


## 데몬 스레드(daemon thread), 일반 스레드(non-daemon thread)
- daemon thread : JVM이 사용하느 스레드, ex) garbage collection thread
- non-daemon thread : 응용프로그램에서 생성한 스레드
- JVM은 non-daemon thread가 하나 이상 살아있으면 실행을 계속 함


## Thread 생명 주기

`NEW` : 생성, 실행할 준비 X
`RUNNABLE` : 현재 실행되고 있거나 스케줄링 기다리는 중
`WAITING` : `notify()` 혹은 `notifyAll()`을 불러주기 기다리고 있는 상태, 스레드 동기화를 위해 사용됨
`TIMED_WAITING` : 잠 자고 있는 상태
`BLOCK` : IO 작업을 요청해 IO 작업이 완료되기를 기다리는 상태
`TERMINATED` : 스레드가 종료한 상태

## Thread 동기화

- `synchronized` : 진입 시 lock을 걸고 빠져나올 때 unlock하여 스레드 동기화 진행하는 키워드


## wait(), notify(), notifyAll()

- `java.lang.Object`의 스레드를 동기화하는 방법
- `wait()` : 다른 스레드가 notify() 해줄 때 까지 대기
- `notify()` : 대기중인 한 개의 스레드를 RUNNABLE로 만듦
- `notifyAll()` : 대기중인 모든 스레드를 RUNNABLE로 만듦


### 스레드 생성

1. Thread 클래스 이용

- `java.lang.Thread` 이용

```JAVA
(1) Thread 클래스 상속 및 run() 메소드 오버라이딩
class MyThread extends Thread{
  public void run() {
    //do something
  }
}

(2) Thread 객체 생성 및 start()
MyThread th = new MyThread();
th.start();
```

2. Runnable 인터페이스 이용

```JAVA
interface Runnable() {
  public void run();
}

(1) Runnable 인터페이스 구현
class MyRunnable implements Runnable{
  public void run() {
    // do something
  }
}

(2) 스레드 객체 생성 및 start()
Thread th = new Thread(new MyRunnable());
th.start();
```
