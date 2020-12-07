# RxJava



## Hot Observable, Cold Observable

- Observable에는 hot, cold 두가지가 있음
- 일반적으로 우리가 사용한건 cold
- cold는 Observable을 생성하고 Observer가 subscribe를 호출할 때까지 데이터 발행 안함 --> lazy함



### hot observable

- Observer의 존재 여부와 관계없이 데이터 발행
- Observer는 Observable이 발행하는 데이터 처음부터 끝까지 다 받을수있지는 않음, 보장못함
- Observer는 구독한 시점부터 데이터 받음



cold observable 예시 : 웹 요청, DB 쿼리, 파일 읽기

hot observable 예시 : 마우스 이벤트, 키보드 이벤트, 시스템 이벤트 ..., 센서 데이터



### 주의할 점

- hot boservable은 back pressure를 고려해야함
- back presure는 데이터를 발행하는 속도와 구독자가 처리하는 속도의 차이가 클때 발생



### cold -> hot

- cold observable을 hot observable로 바꿔주는 거에는 Subject, ConnectableObservable이 있음
- 주요 Subject 클래스 : AsyncSubject, BehaviorSubject, PublishSubject, ReplaySubject