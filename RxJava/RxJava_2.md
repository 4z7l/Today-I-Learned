# RxJava

1. Reactive Programming 이란
2. **Observable**
3. 연산자
4. 스케줄러
5. RxAndroid



# Observable

- 데이터 흐름에 맞게 알림을 보내 구독자가 데이터를 처리할 수 있도록 함
- RxJava의 핵심임
- Observer Pattern 구현 : 객체의 상태 변화를 관찰하는 Observer 목록을 객체에 등록, 상태 변화가 있을 때마다 메소드를 호출하여 옵서버에게 변화 알려줌



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
