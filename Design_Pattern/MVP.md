# MVP (Model-View-Presenter)

## MVP란

### Model
- 데이터 저장, 처리
- View, Presenter에 독립적
### View
- Model에서 처리된 데이터를 Presenter로부터 받음
- 사용자의 입력을 받아 Presenter에 보냄
- Presenter에 의존적
- EX) Activity, Fragment
### Presenter
- Model과 View 사이 매개체
- View로부터 사용자 입력을 전달받아 Model의 로직 호출
- Model의 처리 결과를 전달받아 View로 전달



# 구글 로그인 MVP

## 요구사항 분석
### (1) 요구사항 분석
1. 현재 로그인되어있는지 확인
2. 구글 로그인 버튼을 누르면 사용자 인증정보에 연결됨
3. 인증이 유효하면 유저 정보를 담아 MainActivity로 이동
4. 인증이 유효하지 않으면 에러 메시지 보여줌

### (2) 세분화
#### 1. 현재 로그인되어있는지 확인
- M : 구글 로그인 정보를 받아온다(Firebase에 인증하여 성공/실패 결과를 P에게 전달)
- P : 로그인 정보를 SocialLoginActivity로 전달

#### 2. 구글 로그인 버튼을 누르면 사용자 인증정보에 연결됨
- V : Presenter로부터 로그인 정보 받음 -> [로그인 정보 유효 -> MainActivity / 유효x -> 그대로]

#### 3-1. 인증이 유효한지 확인
- V : 사용자가 버튼을 클릭하면 이를 감지하여 presenter에 보냄
- P : V에 입력이 들어왔음을 전달받아 M 호출
- M : Firebase에 인증하여 성공/실패 결과를 P에게 전달

#### 3-2. 결과에 따라 View update
- P : M의 로직 호출 결과를 V에게 전달
- V : 결과를 기반으로 UI update



## 구현 방법
#### (1) [Google Architecture]([https://github.com/android/architecture-samples](https://github.com/android/architecture-samples))
- Contract : View와 Presenter에 대한 interface 구현
- Presenter : Contract.Presenter를 상속받아 구현
- View : Contract.View를 상속받아 구현

#### (2) 생성 방법
- Presenter : 실제 View가 만들어지는 시점에 생성 후 setView
- setView가 호출되는 시점에 setPresenter(this)
- View : setPresenter를 통해 전달받은 presenter를 통해 처리

#### (3) 좋은 MVP 구현
- BaseView, BasePresenter, BaseActivity를 만듦
- Presenter에서는 View를 모르게
- View에서는 if문 등을 아예 없애고 Presenter에서는 Android API를 모르게



## [결과](https://github.com/4z7l/architecture-study/tree/4z7l/MVP)


<br><br>

> :bookmark: REFERENCE   
> [MVP 패턴 코틀린으로 작업](https://devbearkinf.tistory.com/27)     
> [안드로이드 어플리케이션에 MVP패턴을 적용하는 방법](https://brunch.co.kr/@mobiinside/913)    
> [Android MVP 무작정 따라하기 - Presenter/View 생성하기](https://thdev.tech/androiddev/2016/11/28/Android-MVP-One/)    
> [MVP (Model View Presenter) 패턴의 로그인 예](https://riptutorial.com/ko/android/example/16219/mvp--model-view-presenter--%ED%8C%A8%ED%84%B4%EC%9D%98-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%98%88)   
>  [correct work with onActivityResult in MVP project](https://stackoverflow.com/questions/48438754/correct-work-with-onactivityresult-in-mvp-project)   
> [ Implement interaction onActivityResult method from Activity to Presenter](https://github.com/LiveTyping/u2020-mvp/issues/14)    
> [renanalmeida/KotlinMVP](https://github.com/renanalmeida/KotlinMVP)