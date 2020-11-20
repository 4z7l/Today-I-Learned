# Rx (Reactive eXtension)
- 관찰 가능한 시퀀스를 사용하여 비동기식 및 이벤트 기반 프로그램을 구성하기 위한 라이브러리
- 환경이 변하면 이벤트를 받음
- 네트워크 작업이 짧다면 상관없지만 오래 걸리는 경우가 많기 때문에 비동기 처리를 해야함
- 데이터 흐름을 먼저 정의하고 데이터가 변경되었을 때 연관되는 함수나 메서드가 자동으로 업데이트 되는 방식
- __observer__ 패턴 사용

### 비동기
- 메인스레드의 동작을 방해하지 않고 뒤에서 처리하는 작업을 비동기라함
- 주 프로그램 흐름과 독립적
- 너무 많은 thread 사용하면 안됨 -> WHY? -> deadlock 가능성

### 데이터 스트림 (Data Stream)
- 말그대로 데이터의 흐름임
- 클릭이벤트, http request, 값의 변화, 캐시 이벤트, 센서에서 측정된 값 등 모든 것들을 데이터 스트림으로 만듦
- Stream을 Observable이라 표현함

## 4가지 ReactiveX 원칙

#### 1. Responsive
- 사용자에게 즉각적으로 반응
- 이를 위해선 시스템이 __메시지 구동 방식__ 이어야함
#### 2. Resilient (탄력성)
- 일반적인 상황뿐만 아니라 장애 등의 상황에서도 응답성을 보장해야함
#### 3. Elastic
- 탄력성과 유연성은 함께 작용함 -> 응답성 보장
#### 4. Message-driven
- Reactive는 메시지 기반이어야함
> - 메시지 : 특정 대상으로 보내지는 데이터 항목
> - 이벤트 : 주어진 상태에 도달했을 때 구성요소가 내보낸 신호


## Rx가 쓰이는 상황
- 마우스 움직임, 버튼 클릭과 같은 UI 이벤트
- 속성 변경, 컬렉션 업데이트, 주문 완료, 등록 승인 등의 도메인 이벤트
- 메시지 버스의 브로드캐스트처럼 대기 시간이 짧은 미들웨어의 푸시 이벤트

## 종류
1. RxAndroid
- RxLifecycle : RxJava를 사용하는 안드로이드 앱용 라이프 사이클 처리 API
- RxBinding : 안드로이드 UI 위젯용 RxJava 바인딩 API
- RxPermissions : RxJava에서 제공하는 안드로이드 런타임 권한 라이브러리

2. RxJava
- Rx의 자바 버전, 비동기 data stream 생성 가능
- 아무 thread에서 비동기 data stream 생성 가능, 아무 thread에서 observer가 data 소비 가능

3. RxKotlin
- Rx의 코틀린 버전
- Rxjava를 코틀린으로 사용할 수 있음


## 구성요소

### Observable과 Observer
- rx는 observer 패턴을 베이스로 함
- __Observable__ 이 emit -> __Observer(Subscriber)__ 가 consume
- Observable이 데이터를 방출할 때 마다 등록된 모든 Observer가 데이터를 수신한다.
- Observable이 데이터를 가짐 , Observer가 그 데이터를 가지고 어떻게 행동해야할지 정의(?)
- Observable이 __언제, 무엇을__ emit하는지 선언하기 위해 subscribe를 함?
- Observer에서 수신하는/ Observable이 제공하는 3가지 Callback
	+ `onNext` : 새로운 데이터 전달
	+ `onCompleted` : 스트림 종료, 더이상 이벤트 보낼 수 없음
	+ `onError` : 에러 신호 전달

<br>

### Observable의 종류?!
-   `Observable` : 최상위 기본타입.
-   `Single` : 1개의 데이터만 반환
-  `Maybe` : Null 가능성 있는 1개의 데이터 반환
-   `Completable` : 반환값 없이 수행 후 종료
-   `Flowable` : Backpressure


### 함수
 https://nittaku.tistory.com/213

- `filter` : 특정 이벤트일 때만 행동 (ex. 문자열이 있을때만 true)
> ```
> Observable.just(query)  .filter(text  ->  !TextUtils.isEmpty(text))
> ```

- `map` : 입력으로 들어 오는 값을 변경 할 수 있다

> ```
> Observable.just(query)
> 	.map(text -> "간장공장"+text)
> ```

- `zip` : 두 개 이상의 Observable 결합, 만약 한쪽의 Observable이 처리가 안되었다면 처리가 될 때까지 대기

- `combineLatest()` : 2개 이상의 Observable을 기반으로 Observable 각각의 값이 변경됐을 때 갱신

- `merge()` : 2개 이상의 Observable을 한번에 방출, __단,__ 먼저 오면 먼저 방출

- `switchMap()` : 순서 보장하지만 중간에 다른거 발행되면 그걸로 처리함


# RxJava

## 예시코드

https://ojh102.tistory.com/1

```java
Observable
    // create 부분
    .create(new ObservableOnSubscribe<String>() {
        @Override
        public void subscribe(ObservableEmitter<String> emitter) {
            final List<String> values = Arrays.asList("hello", "rx", "world");
​
			//데이터 발행
            for(String value: values) {
                emitter.onNext(value);
            }
​			//데이터 발행 후 스트림이 끝났음을 알림
            emitter.onComplete();
        }
    })
    // combine 부분
    .map(new Function<String, String>() {
        @Override
        public String apply(String s) {
	        // 들어온 값 정제
            return s + "!";
        }
    })
    // 데이터 스트림 사용하는 부분 -> consumer니까 데이터 스트림을 소비하겠지?!
    .subscribe(
		    //onNext에서 emit한 값 받음
            new Consumer<String>() {
                @Override
                public void accept(String s) {
                    System.out.println(s);
                }
            },
            //onError에서 emit한 Throwable 다룸
            new Consumer<Throwable>() {
                @Override
                public void accept(Throwable throwable) {
                    System.out.println(throwable.toString());
                }
            },
            //onCompleted에서 완료됐음을 전달받음
            new Action() {
                @Override
                public void run() {
                    System.out.println("complete");
                }
            }
    );
```


# RxBinding
- 안드로이드의 위젯이나 View를 구독할 수 있게 해주는 오픈소스
- Activity가 사라졌을 경우 Subscribe 해제해야함!!!!
-> 안할 경우 __Memory Leak__ 발생할수도 있음..
> 1. Subscription 사용 (https://fisache.github.io/rxstudy-rxbinding-1/)
> 2. RxLifeCycle library 사용 (https://tourspace.tistory.com/300)
> 3. CompositeDisposable 사용 -> `CompositeDisposable.add()`  함수를 통해 disposable을 등록시키고 `CompositeDisposable.clear()`  로 등록된 subscriber를 한번에 해제 시킬수 있음  

## TextWatcher

- 그냥 view에서는 `click` , textview에서는 `textChanges` 쓰는듯??

```kotlin
fun processTextWatcher(tv: TextView) {
	val observable = tv.textChanges()
	observable.subscribe {
		charSequcne -> Toast.makeText(context, charSequcne.toString(), Toast.LENGTH_SHORT)
	}
}
```

## 예시코드

### 원래
```java
Button button = (Button)findViewById(R.id.button);
button.setOnClickListener(new View.OnClickListener() {
   @Override
   public void onClick(View v) {
      //handle on click here
   }
});
```

### RxBinding 사용 (unsubscribe 필수 ㅡㅡ!)
```java
Button button = (Button)findViewById(R.id.button);
Subscription buttonSub = RxView.clicks(button).subscribe(new Action1<Void>() {
   @Override
   public void call(Void aVoid) {
      //handle on click here
   }
});

```

```java
EditText editText = (EditText)findViewById(R.id.editText);
Subscription editTextSub = RxTextView.textChanges(editText).subscribe(new Action1<CharSequence>() {
   @Override
   public void call(CharSequence value) {
      // do some work with new text
   }
});
```

### 예시
```java
RxTextView.textChanges(searchTextView)
	.filter(new Func1<String, Boolean> (){
		@Override
		public Boolean call(String s) {
			return s.length() > 2;
			// 길이 2이상인 것만
		}
	})
	.debounce(100, TimeUnit.MILLISECONDS) //빠른 연속 이벤트의 흐름 제어 -> 100초의 간격이 있는데 그 중 마지막 데이터에 대해서만 처리하는듯
	.switchMap(new Func1<String, Observable<List<Result>>>() {
		makeApiCall(s);	//마지막 데이터에 대해 무언가 함
	})
	.subscribeOn(Schedulers.io())	//스케줄러를 io로 지정
	.observeOn(AndroidSchedulers.mainThread())	//메인스레드로 지정
	.subscribe(/* attach observer */);
```

## Room에서 비동기처리할때 반환값
![image](https://miro.medium.com/max/875/0*jEnmX0FZOBDdJIHK)
https://medium.com/androiddevelopers/room-flow-273acffe5b57



<br><br><br>

> :bookmark: __REFERENCE__
> https://jeongupark-study-house.tistory.com/133<br>
> https://juyoung-1008.tistory.com/38<br>
> https://m.blog.naver.com/jdub7138/220983291803<br>
> https://choonguri.github.io/2017/07/19/5-things-to-know-about-reactive-programming.html<br>
> https://medium.com/@jang.wangsu/rxswift-rxswift%EB%9E%80-reactivex-%EB%9E%80-b21f75e34c10<br>
> https://ojh102.tistory.com/1<br>
> https://guides.codepath.com/android/RxJava-and-RxBinding<br>
