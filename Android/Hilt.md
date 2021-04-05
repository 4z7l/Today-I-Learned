# Hilt

## 사용법

1. Hilt Application 클래스 생성

```kotlin
@HiltAndroidApp
class ExampleApplication : Application() { ... }
```

- `@HiltAndroidApp` : Hilt 코드 생성 발생시킴, `@AndroidEntryPoint`가 있는 안드로이드 클래스에 DI 가능해짐
  +  `Application`, `Activity`, `Fragment`, `View`, `Service`, `BroadcastReceiver`에 의존성 주입 가능


2. @Inject로 주입하기 - 생성자 삽입

```kotlin
class AnalyticsAdapter @Inject constructor(
  private val service: AnalyticsService
) { ... }
```

```kotlin
@AndroidEntryPoint
class ExampleActivity : AppCompatActivity() {

  @Inject lateinit var analytics: AnalyticsAdapter
  ...
}
```

- `@Inject` : 생성자에 주입해라


3. @Module로 주입하기 - 생성자 삽입 불가능한 경우(ex. 인터페이스)

- `AnalyticsService` 인터페이스를 사용해야할 때 @Module
- `AnalyticsServiceImpl`는 생성자 주입으로 받음
- `@InstallIn(ActivityComponent::class)` : `AnalyticsModule` 을 모든 Activity에서 사용 가능함

```kotlin
interface AnalyticsService {
  fun analyticsMethods()
}

// Constructor-injected, because Hilt needs to know how to
// provide instances of AnalyticsServiceImpl, too.
class AnalyticsServiceImpl @Inject constructor(
  ...
) : AnalyticsService { ... }

@Module
@InstallIn(ActivityComponent::class)
abstract class AnalyticsModule {

  @Binds
  abstract fun bindAnalyticsService(
    analyticsServiceImpl: AnalyticsServiceImpl
  ): AnalyticsService
}
```
