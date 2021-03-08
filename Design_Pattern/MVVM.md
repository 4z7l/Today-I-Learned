# 2주차 : MVVM

![The MVVM pattern](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/enterprise-application-patterns/mvvm-images/mvvm.png)
![Image for post](https://miro.medium.com/max/522/1*oW2OtsU4itFE-1njkwJ06w.png)

![](https://blog.yena.io/assets/post-img19/190316-mvvm-detail.png)

> ## MVVM

Model + View + ViewModel
ViewModel이 Model의 데이터를 참조 -> View는 상태 변화를 감지하여 화면 갱신

- View->ViewModel->Model
- View : ViewModel = n : m
- ViewModel은 context를 참조하면 안됨
- Model은 Repository 패턴으로 만듦
- RxJava의 `Observable` 을 이용

### Model
- 데이터 저장, 처리
- ViewModel이 요청하는 데이터 준비
- Model은 ViewModel을 모른다
### View
- 비즈니스 로직 미포함
- ViewModel을 Binding하여 ViewModel을 관찰하다 상태 변화 전달 시 화면 갱신
- EX) Activity, Fragment
### ViewModel
- View가 데이터바인딩 할 수 있는 속성과 명령으로 구성
- ViewModel은 Model을 알고, View를 모른다
- View에 대한 Reference를 가지지 않음

> ## AAC

### Room
- SQLite를 편리하게 사용하도록 도와줌

### Databinding
- 데이터를 xml에서 처리하도록 도와줌

### Repository
- 내장 데이터베이스나 외부 웹 서버 등에서 데이터를 가져옴
- 뷰모델은 DB나 서버에 직접 접근하지 않고, 리포지토리에 접근하는 것으로 앱의 데이터를 관리

### LiveData 
- 관찰이 가능한(Observable) 데이터 홀더 클래스
- 뷰에서 뷰모델의 라이브데이터를 관찰하게 되면 데이터가 변경될 때 내부적으로 자동으로 알려줌
-  액티비티나 프래그먼트의 생명 주기를 인지
- 최신 데이터 유지
- 메모리 누수 x

> ## MVVM의 장점
- 뷰가 데이터를 실시관으로 관찰 : Observable 패턴 이용
- 생명주기와 독립적
- 모듈화로 유닛테스트 용이


> ## 구현 방법

### Room
![](https://developer.android.com/images/training/data-storage/room_architecture.png?hl=ko)
1. dependency 추가
2. Model, Dao(Data Access Object) 작성
3. Database 작성
- `@Database`
-  `RoomDatabase`를 확장하는 추상 클래스여야 함
-   주석 내에 데이터베이스와 연결된 항목의 목록을 포함
-   인수가 0개이며 `@Dao`로 주석이 지정된 클래스를 반환하는 추상 메서드를 포함
4.  Repository 생성
5.  ViewModel 생성
6.  Activity 설정



## [Todo List - MVVM](https://github.com/4z7l/architecture-study/tree/4z7l/MVVM2)



<br><br>
> :bookmark: REFERENCE   
>  [[Android] 안드로이드 - MVVM 패턴에 대하여](https://lktprogrammer.tistory.com/195)      
>  [[Android] Kotlin + MVVM + AAC 로 Todo 앱 만들기 - 1](https://doitddo.tistory.com/52?category=855312)   
> [[Android] MVVM & 안드로이드 아키텍쳐 컴포넌트 시작하기](https://blog.yena.io/studynote/2019/03/16/Android-MVVM-AAC-1.html)   
> https://github.com/aligokdemir/Android-Todo-List-App-with-MVVM-and-Architecture-Components   
>  [[Android, MVVM] MVVM 따라하기 - 4 (MVVM 구현)](https://black-jin0427.tistory.com/270)   
> [Room을 사용하여 로컬 데이터베이스에 데이터 저장](https://developer.android.com/training/data-storage/room?hl=ko#kotlin)   
> https://blog.yena.io/studynote/2019/03/16/Android-MVVM-AAC-1.html   
> https://blog.yena.io/studynote/2019/03/27/Android-MVVM-AAC-2.html   
> https://developer.android.com/topic/libraries/architecture/adding-components?hl=ko#lifecycle   
> https://developer.android.com/topic/libraries/architecture/livedata?hl=ko   
> https://developer.android.com/topic/libraries/data-binding/start?hl=ko   
> https://developer.android.com/training/data-storage/room/prepopulate?hl=ko   
> https://deque.tistory.com/112?category=984011   
> https://m.blog.naver.com/lcs5382/221788978850   
> https://doitddo.tistory.com/54?category=855312   
> https://github.com/aligokdemir/Android-Todo-List-App-with-MVVM-and-Architecture-Components   
> https://github.com/android/architecture-components-samples/blob/master/BasicRxJavaSampleKotlin/app/src/main/java/com/example/android/observability/ui/UserActivity.kt   
> https://stackoverflow.com/questions/46665621/android-room-persistent-appdatabase-impl-does-not-exist/49323956   
> https://tristan91.tistory.com/475   
> https://0391kjy.tistory.com/37   
> https://github.com/android/architecture-components-samples   
> https://poqw.github.io/about_mvvm/   