# RxJava

## observeOn()과 subscribeOn()의 차이

`subscribeOn()`
- subscribeOn은 Observable 객체가 실행될 쓰레드를 정한다.

- 예를 들면 userApi.getUsers().subscribeOn(newThread()) 으로 사용했다면 getUsers() 가 newThread 안에서 실행됨.


`observeOn()`
- observeOn은 그 다음에 오는 연산이 실행될 쓰레드를 정한다.
- 예를 들면 `userApi.getUsers().subscribeOn(newThread()).observeOn(mainThread()).subscribe({

Log.d("Log", "Logging");

},{},{})` 으로 사용했다면 getUsers() 가 newThread 안에서 실행되고, subscribe() 코드가 메인 쓰레드 안에서 실행된다.

> https://yunhookim.tistory.com/10
