# RxJava

1. Reactive Programming 이란
2. **Observable**
3. 연산자
4. 스케줄러
5. RxAndroid



# Observable

- 데이터 흐름에 맞게 알림을 보내 구독자가 데이터를 처리할 수 있도록 함
- RxJava의 핵심임
- Observer Pattern 구현 : 객체의 상태 변화를 관찰하는 Observer 목록을 객체에 등록, 상태 변화가 있을 때마다 메소드를 호출하여 옵서버에게 변화 알려줌, Observer는 Observable이 발행하는 데이터에 반응한다. 
- Observable은 Pull방식인 Iterable의 Push 방식 class임
- Iterable은 consumer가 값을 pull하고 값이 도착할때까지 thread를 차단함 / Observable은 값이 사용가능하면 consumer에게 값을 push함
- Lifecycle은 없음



Observable <- (subscribe) <- Observer/subscriber/wathcer/reactor



<br>

- 배열과 같은 Collections를 사용할때와 같은 방식으로 비동기 이벤트 스트림을 처리할 수 있음

> The ReactiveX Observable model allows you to treat streams of asynchronous events with the same sort of simple, composable operations that you use for collections of data items like arrays. It frees you from tangled webs of callbacks, and thereby makes your code more readable and less prone to bugs.

<br>

- Java의 Futures는 비동기 실행 가능, 하지만 요청에 대한 지연이 런타임에 달라져서 적절한 비동기 실행 흐름을  구성하기 어렵고 불가능하다. (Futures.get()으로 가능하기는 하지만 비동기의 이익을 제거함)
- Observable은 비동기 데이터의 흐름과 시퀀스를 구성할 수 있음

> ## Observables Are Composable
>
> Techniques like [Java Futures](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Future.html) are straightforward to use for [a single level of asynchronous execution](https://gist.github.com/4670979) but they start to add [non-trivial complexity](https://gist.github.com/4671081) when they’re nested.
>
> It is [difficult to use Futures to optimally compose conditional asynchronous execution flows](https://gist.github.com/4671081#file-futuresb-java-L163) (or impossible, since latencies of each request vary at runtime). This [can be done](http://www.amazon.com/gp/product/0321349601?ie=UTF8&tag=none0b69&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321349601), of course, but it quickly becomes complicated (and thus error-prone) or it prematurely blocks on `Future.get()`, which eliminates the benefit of asynchronous execution.
>
> ReactiveX Observables, on the other hand, are *intended* for [composing flows and sequences of asynchronous data](https://github.com/Netflix/RxJava/wiki/How-To-Use#composition).



<br>

- 단순한 scalar 값 뿐만 아니라 무한한 스트림을 차례로 방출 가능
- Observable은 어떠한 유스케이스에서도 사용가능

> ## Observables Are Flexible
>
> ReactiveX Observables support not just the emission of single scalar values (as Futures do), but also of sequences of values or even infinite streams. `Observable` is a single abstraction that can be used for any of these use cases. An Observable has all of the flexibility and elegance associated with its mirror-image cousin the Iterable.

<br>

- Observable은 스레드풀, 이벤트루프, non-blocking I/O, actors 등 아무렇게나 구현될 수 있다. 

> ## Observables Are Less Opinionated
>
> ReactiveX is not biased toward some particular source of concurrency or asynchronicity. Observables can be implemented using thread-pools, event loops, non-blocking I/O, actors (such as from Akka), or whatever implementation suits your needs, your style, or your expertise. Client code treats all of its interactions with Observables as asynchronous, whether your underlying implementation is blocking or non-blocking and however you choose to implement it.

<br>

- Calback은 single level의 비동기 실행에는 쉽지만, 중첩되면 어려워짐

> ## Callbacks Have Their Own Problems
>
> Callbacks solve the problem of premature blocking on `Future.get()` by not allowing anything to block. They are naturally efficient because they execute when the response is ready.
>
> But as with Futures, while callbacks are easy to use with a single level of asynchronous execution, [with nested composition they become unwieldy](https://gist.github.com/4677544).



<br>

## Subscribe

- 동작을 사전에 정의하고 실행되는 시점을 조절할 수 있음
- 팩토리 함수로 데이터 흐름을 정의한 후 subscribe를 호출해야 실제로 데이터를 발행함
- Observable에 onNext, onError, onComplete가 발생했을 때 실행할 내용 지정
- 인자가 없는건 onError가 발생했을 때만 onErrorNotImplementedException을 throw함 -> 테스트나 디버깅할 때 주로 사용

```java
public final Disposable subscribe()
public final Disposable subscribe(@NonNull Consumer<? super T> onNext)
public final Disposable subscribe(@NonNull Consumer<? super T> onNext, @NonNull Consumer<? super Throwable> onError)
public final Disposable subscribe(@NonNull Consumer<? super T> onNext, @NonNull Consumer<? super Throwable> onError, @NonNull Action onComplete)
public final void subscribe(@NonNull Observer<? super T> observer)
```



## Disposable

- dispose() : Observable이 데이터를 발행하지 않도록 구독 해지, onComplete 보내면 자동으로 dispose호출
- isDisposed() : 구독을 해지했는지 확인하는 함수

```java
public class RxExample {
    public static void main(String[] args){
        Observable observable = Observable.just(1,2,3);
        Disposable disposable = observable.subscribe(o -> {
           System.out.println("onNext : "+o);
        }, throwable -> {
            System.out.println("onEror : "+throwable);
        }, () -> {
            System.out.println("onComplete");
        });
        System.out.println("Disposed = "+disposable.isDisposed());
    }
}

출력
onNext : 1
onNext : 2
onNext : 3
onComplete
Disposed = true
```





## 종류

RxJava3 : Observable, Single, Completable, Maybe, Flowable

- [`io.reactivex.rxjava3.core.Flowable`](http://reactivex.io/RxJava/3.x/javadoc/io/reactivex/rxjava3/core/Flowable.html): 0..N flows, supporting Reactive-Streams and backpressure
- [`io.reactivex.rxjava3.core.Observable`](http://reactivex.io/RxJava/3.x/javadoc/io/reactivex/rxjava3/core/Observable.html): 0..N flows, no backpressure,
- [`io.reactivex.rxjava3.core.Single`](http://reactivex.io/RxJava/3.x/javadoc/io/reactivex/rxjava3/core/Single.html): a flow of exactly 1 item or an error,
- [`io.reactivex.rxjava3.core.Completable`](http://reactivex.io/RxJava/3.x/javadoc/io/reactivex/rxjava3/core/Completable.html): a flow without items but only a completion or error signal,
- [`io.reactivex.rxjava3.core.Maybe`](http://reactivex.io/RxJava/3.x/javadoc/io/reactivex/rxjava3/core/Maybe.html): a flow with no items, exactly one item or an error.





## 1. observable

- 0개 이상의 flow, backpressure 없음
- 세 가지의 알림을 구독자에게 전달
- `onNext()` : Observable 데이터의 발행
- `onComplete()` : 데이터의 발행이 완료됨, 단 한번만 발생, 이 이후에는 onNext가 오면 안됨
- `onError()` : Observable에서 에러가 발생함, 이후에 onNext나 onComplete가 발생하지 않음



### just()

- 인자로 넣은 데이터(최대 10개까지 가능)를 차례로 자동 발행
- 데이터를 변경하지 않고 그대로 발행

```java
Observable.just("hi")
                .subscribe(System.out::println);
```



### create()

- 인자로 데이터 넣고 onNext, onError, onComplete를 직접 호출해야함

```java
Observable.create(emitter -> {
            emitter.onNext(1);
            emitter.onNext(2);
            emitter.onComplete();
        })
        .subscribe();
```

- 단, 사용할 때 주의해야함 -> Rxjava에 익숙한 사람만 쓰기를 권고함
- 왜? -> Observable이 dispose됐을때 등록된 콜백을 모두 해제해야함, 안하면 메모리누수
- 구독자가 구독하는 동안에만 onNext, onComplete 호출해야함
- 에러 발생시 onError로만 에러 전달
- back pressure 직접 처리



### fromXXX()

- fromArray()
- fromIterable()
- fromCallable()
- fromFuture()
- fromPublisher()



- [**`Create`**](http://reactivex.io/documentation/operators/create.html) — create an Observable from scratch by calling observer methods programmatically
- [**`Defer`**](http://reactivex.io/documentation/operators/defer.html) — do not create the Observable until the observer subscribes, and create a fresh Observable for each observer
- [**`Empty`/`Never`/`Throw`**](http://reactivex.io/documentation/operators/empty-never-throw.html) — create Observables that have very precise and limited behavior
- [**`From`**](http://reactivex.io/documentation/operators/from.html) — convert some other object or data structure into an Observable
- [**`Interval`**](http://reactivex.io/documentation/operators/interval.html) — create an Observable that emits a sequence of integers spaced by a particular time interval
- [**`Just`**](http://reactivex.io/documentation/operators/just.html) — convert an object or a set of objects into an Observable that emits that or those objects
- [**`Range`**](http://reactivex.io/documentation/operators/range.html) — create an Observable that emits a range of sequential integers
- [**`Repeat`**](http://reactivex.io/documentation/operators/repeat.html) — create an Observable that emits a particular item or sequence of items repeatedly
- [**`Start`**](http://reactivex.io/documentation/operators/start.html) — create an Observable that emits the return value of a function
- [**`Timer`**](http://reactivex.io/documentation/operators/timer.html) — create an Observable that emits a single item after a given delay



- `Create` : onNext, onError, onCompleted를 사용해 Observable을 처음부터 생성 가능
- `Defer` : Observer가 구독할 때 까지 기다렸다가 구독하면 그때 Observable을 생성함
- Empty : 아이템 0개 방출, 정상 완료
- `Never` : 아이템 0개 방출, 종료하지 않음
- `Throw` : 아이템 0개 방출, 에러
- `From` : 다른 객체를 Observable로 변환
- `Interval` : 시간간격을 두고 데이터를 방출하는 Observable 생성
- `Just` : 전달한 아이템을 그대로 방출
- `Range` : 특정 범위 내의 Integer 형태의 아이템 방출
- `Repeat` : 특정 횟수만큼/ 무한히 반복하여 방출
- `Start` : 특정 값을 반환하는 Observable을 방출, 함수처럼 작용
- `Timer` : delay 후 아이템 방출





## 2. Single

- 오직 1개의 데이터만 발행
- 보통 결과가 유일한 서버 API를 호출할 때 사용
- 발행과 동시에 종료됨
- onSuccess와 onError만 있음



### just()

- 가장 간단한 Single 생성 방법

```java
Single<String> single = Single.just("HI");
        single.subscribe();

```



### Observable에서 변환 가능

- Single.fromObservable()
- Observable.single()
- Observable.first()
- Observable.empty().single()
- Observable.just().take(1).single()



## 3. Maybe

- 0개 or 1개
