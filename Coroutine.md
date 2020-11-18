# Coroutine

- 안드로이드에서 비동기 실행을 도와주는 디자인 패턴, 패러다임
- 코틀린에만 존재하는 개념이 아님
- long-running task을 관리하도록 도와줌
- 동시성 프로그래밍 가능
- thread가 여러개면 thread가 매번 CPU를 선점하며 context switch가 발생 --> coroutine은 하나의 스레드로 코루틴 여러개가 동시성 프로그래밍을 하며 context switch를 하지 않음
- 함수가 coroutine builder를 만나 coroutine이 되면 함수를 왔다 갔다 할 수 있음 -> 함수가 suspend(일시중지)&resume(재개)될 수 있음
- **쓰레드**의 **문맥 교환**은 프로세스 문맥 교환과는 달리 **캐시 메모리를 비울 필요**가 없기 때문에 더 빠르다.



## 기능

(1) suspension을 지원하므로 싱글 스레드에서 많은 코루틴 사용 가능

- suspension : 코루틴이 실행될때 스레드를 block하지 않음 -> 메모리 절약

(2) 메모리 누수 감소

(3) 취소 시 실행중인 코루틴 계층에서 자동으로 전파됨



## 관련 용어

### Scope

- `CoroutineScope` : 코루틴의 범위, 코루틴을 제어할 수 있는 단위
- `viewModelScope` : ViewModel에 있는 CoroutineScope KTX
- Scope : 코루틴은 scope 내에서 실행되어야 함
- ex) 만약 코루틴이 viewmodelscope에서 실행되고 있는 경우, viewmodel이 destroy되면 실행되면 코루틴도 취소됨

### Coroutine Context

- job, dispatcher가 있음

| `Dispatcher.Default` | CPU 사용량이 많은 작업      |
| -------------------- | --------------------------- |
| `Dispatcher.IO`      | 네트워크, 디스크 사용 작업  |
| `Dispatcher.Main` :  | 안드로이드의 경우 UI 스레드 |

### launch

- `launch`와 `async`는 코루틴을 만들고 실행해주는 코루틴 빌더

- `launch` : 코루틴 생성, dispatcher에 코드를 dispatch(파견)함, `Job` 반환
- `async` : `Deferred` 반환
- `Job` : 실행, `Deferred` : 실행 후 값 반환
- 다음 코드가 수행될때까지 대기 : `Job.join()`, `Deferred.await()`



## 기본 사용법

(1) 사용할 Dispatcher 결정

(2) CoroutineScope 생성

(3) CoroutineScope의 launch/async에 코드 작성



## 예제 - 

```kotlin
val scope = CoroutineScope(Dispatchers.Main)

    scope.launch {
        // 포그라운드 작업
    }

    scope.launch(Dispatchers.Default) {
        // CoroutineContext 를 변경하여 백그라운드로 전환하여 작업을 처리합니다
    }

	CoroutineScope(Dispatchers.Default).launch {
        // 새로운 CoroutineScope 로 동작하는 백그라운드 작업
    }

    scope.launch(Dispatchers.Default) {
        // 기존 CoroutineScope 는 유지하되, 작업만 백그라운드로 처리
    }	
```





## 예제 - 공식 문서

- `withContext()` : 코루틴이 다른 thread에서 실행되도록 함
- `suspend` : 함수가 코루틴 내에서 실행될 수 있도록 강제하는 키워드, suspend가 붙은 함수는 코루틴 내에서 실행되어야 함

```kotlin
class LoginRepository(...) {
    ...
    suspend fun makeLoginRequest(
        jsonBody: String
    ): Result<LoginResponse> {

        // Move the execution of the coroutine to the I/O dispatcher
        return withContext(Dispatchers.IO) {
            // Blocking network request code
        }
    }
}
```

```kotlin
class LoginViewModel(
    private val loginRepository: LoginRepository
): ViewModel() {

    fun login(username: String, token: String) {

        // 메인 스레드에 새로운 코루틴 생성
        viewModelScope.launch {
            val jsonBody = "{ username: \"$username\", token: \"$token\"}"

            // 끝날때까지 임의로 일시중단이 가능한 함수 실행
            val result = try {
                loginRepository.makeLoginRequest(jsonBody)
            } catch(e: Exception) {
                Result.Error(Exception("Network request failed"))
            }

            //withContext가 끝나면 여기서부터 login() 재개
            // 결과 display
            when (result) {
                is Result.Success<LoginResponse> -> // Happy path
                else -> // Show error in UI
            }
        }
    }
}
```











> [코틀린 코루틴(coroutine) 개념 익히기](https://wooooooak.github.io/kotlin/2019/08/25/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%BD%94%EB%A3%A8%ED%8B%B4-%EA%B0%9C%EB%85%90-%EC%9D%B5%ED%9E%88%EA%B8%B0/)<br>
> [Android의 Kotlin 코루틴](https://developer.android.com/kotlin/coroutines?hl=ko)<br>
>
> https://wooooooak.github.io/kotlin/2019/08/25/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%BD%94%EB%A3%A8%ED%8B%B4-%EA%B0%9C%EB%85%90-%EC%9D%B5%ED%9E%88%EA%B8%B0/<br>
>
> https://wooooooak.github.io/kotlin/2019/03/17/kotlin_coroutin/<br>
>
> https://developer.android.com/kotlin/coroutines<br>
>
> https://medium.com/@limgyumin/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%BD%94%EB%A3%A8%ED%8B%B4%EC%9D%98-%EA%B8%B0%EC%B4%88-cac60d4d621b
>
> <br>
>
> https://blog.naver.com/mym0404/221603580011<br>

