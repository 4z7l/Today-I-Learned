# Rx
- 환경이 변하면 이벤트를 받음
- 네트워크 작업이 짧다면 상관없지만 오래 걸리는 경우가 많기 때문에 비동기 처리를 해야함
- 데이터 흐름을 먼저 정의하고 데이터가 변경되었을 때 연관되는 함수나 메서드가 자동으로 업데이트 되는 방식
- observer 패턴 사용

## Rx가 쓰이는 상황
- 마우스 움직임, 버튼 클릭과 같은 UI 이벤트
- 속성 변경, 컬렉션 업데이트, 주문 완료, 등록 승인 등의 도메인 이벤트
- 메시지 버스의 브로드캐스트처럼 대기 시간이 짧은 미들웨어의 푸시 이벤트


## 구성요소
- rx는 observer 패턴을 베이스로 함
- __Observable__ 이 emit -> __Observer(Subscriber)__ 가 consume
- Observable이 데이터를 가짐 , Observer가 그 데이터를 가지고 어떻게 행동해야할지 정의(?)
	+ `onNext` : 새로운 데이터 전달
	+ `onCompleted` : 스트림 종료, 더이상 이벤트 보낼 수 없음
	+ `onError` : 에러 신호 전달
	
-   `Observable` : 최상위 기본타입.
-   `Single` : 1개의 데이터만 반환
-  `Maybe` : Null 가능성 있는 1개의 데이터 반환
-   `Completable` : 반환값 없이 수행 후 종료
-   `Flowable` : Backpressure


# RxBinding
- 안드로이드의 위젯이나 View를 구독할 수 있게 해주는 오픈소스
- Activity가 사라졌을 경우 Subscribe 해제해야함
> 1. Subscription 사용 (https://fisache.github.io/rxstudy-rxbinding-1/)
> 2. RxLifeCycle library 사용 (https://tourspace.tistory.com/300)
> 3. CompositeDisposable 사용 -> `CompositeDisposable.add()`  함수를 통해 disposable을 등록시키고 `CompositeDisposable.clear()`  로 등록된 subscriber를 한번에 해제 시킬수 있음  


## 함수
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






