# Gradle

- build automation tool
- Groovy랑 Kotlin DSL 사용해서 만듦

## 특징

1. High performance : input이나 output이 변경되었을때만 task를 실행해서 불필요한 작업 방지, 빌드 캐시 사용
2. JVM foundation : JVM 위에서 실행됨, gradle 사용하려면 JDK가 설치되어야함
3. Conventions : convention을 구현해서 빌드하기 쉬움, slim한 build script
4. Extensibility : gradle을 확장해서 새로운 task type 만들수 있음 → 안드로이드처럼
5. IDE Support
6. Insight

## Five things you need to know about Gradle

1. Gradle is a general-purpose build tool

- 아무 소프트웨어나 만들수 있음
- 주목할만한 제약 : Maven, Ivy-compatible 레포지토리랑 파일시스템에만 의존성 관리를 지원함
- Gradle 플러그인으로 컨벤션이랑 사전에 만들어진 기능을 사용해서 프로젝트 빌드 가능
- 커스텀 플러그인도 만들수있음

1. The core model is based on tasks

- Gradle은 빌드를 DAG(방향 비순환 그래프, Directed Acyclic Graph)로 모델링함
- 빌드는 의존성에 기반해서 task의 세트로 구성됨
- 그래프가 생성되면 어느 task가 실행되어야할지 경하고 실행함

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b218722-3e2d-4d28-a643-47caccb49952/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b218722-3e2d-4d28-a643-47caccb49952/Untitled.png)

<Task>

- Action : 파일 복사/ 컴파일과 같은 일
- Input : Action이 사용하고 작동시키는 Value, File, directoty
- Output : Action이 수정하고 생성하는 file이나 diectory

1. Gradle has several fixed build phases

- 빌드 스크립트를 3단계로 나눠서 실행함
- imperative(명령형) << delarative(선언형)

```java
"여기 수원인데 강남까지 어케가요"

- 명령형 방식(HOW) : 경부고속도로 타. 경부고속도로 타서 1번 국도 타. 국도에서 빠져나와서 우회전해.
삼거리 나오면 좌회전 해. 
- 선언형 방식(WHAT) : 여기는 경기도 수원시 영통구 센트럴타운로야.
```

1. Initialization 초기화

   빌드 환경 설정 및 빌드에 참여할 프로젝트 결정

2. Configuration

   빌드에 대한 작업 그래프를 구성 및 구성한 다음 사용자가 실행할 작업에 따라 실행할 작업과 순서를 결정한다.

3. Execution 실행

   2단계에서 선택한 task 실행

4. Gradle is extensible in more ways than one

- task type 커스텀 : buildSrc 디렉토리나 packaged plugin에 넣으면 됨
- task action 커스텀 : Task.doFirst() Task.doLast()로 task 로직 커스텀

1. Build scripts operate against an API

- 빌드 스크립트≠ 코드
- 빌드 스크립트에 imperative logic을 피해라
- 그래들이 JVM위에서 실행되기때문에 빌드스크립트로 JAVA API 사용 가능, 코틀린 빌드 스크립트도 코틀린 API 사용 가능, 그루비면 그루비API 사용 가능

## 빌드 캐시

다른 빌드에서 생성된 output 재사용, input이 변경 안됨?→ 그럼 저장된 output 가져옴