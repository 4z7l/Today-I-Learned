# RxJava



## subscribeOn

- 데이터 흐름이 발생하는 스레드 지정
- 여러번 호출해도 처음 지정한 스레드로 고정





## observeOn

- 처리된 결과를 구Observer에게 전달하는 스레드 지정
- 여러번 호출할 수 있으며 호출하는 그 다음부터 스레드를 새롭게 지정ㅎ가능





## observeOn()과 subscribeOn()의 차이

`subscribeOn()`
- subscribeOn은 Observable 객체가 실행될 쓰레드를 정한다.

- 예를 들면 userApi.getUsers().subscribeOn(newThread()) 으로 사용했다면 getUsers() 가 newThread 안에서 실행됨.


`observeOn()`
- observeOn은 그 다음에 오는 연산이 실행될 쓰레드를 정한다.

- 예를 들면



```
userApi.getUsers()
    .subscribeOn(newThread())
    .observeOn(mainThread())
    .subscribe({
        Log.d("Log", "Logging");
        },{

        },{

        }
    )
```

` `

으로 사용했다면 getUsers() 가 newThread 안에서 실행되고, subscribe() 코드가 메인 쓰레드 안에서 실행된다.



![img](http://reactivex.io/documentation/operators/images/schedulers.png)





> https://yunhookim.tistory.com/10
