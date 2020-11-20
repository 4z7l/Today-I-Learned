# DI (Dependency Injection)

## DI란?
- 어떤 객체가 다른 객체의 인스턴스를 가진다면 __의존성__ 을 가진다고 함
- __의존성 주입__ 은 __내부__ 에서 객체를 생성하여 이용하는 것이 아닌, __외부__ 에서 의존성 객체를 생성하여 넘겨주는것
- 클래스 간의 결합도(coupling)를 줄여줄 수 있음
> 모듈간 결합도가 높은 경우 하나의 모듈이 변경되면 그거에 의존하는 다른 모듈까지 변경해주어야함 -> __귀찮음__


## DI의 장점
1. Unit Test 용이
2. 코드의 재사용성 증가
3. refactoring 수월
4. 객체 간의 의존성, 결합도 낮춤
5. 보일러 플레이트 코드 감소
> :bulb: __보일러 플레이트 코드__ : 최소한의 변경으로 여러곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드 (ex. java의 getter, setter),  보일러 플레이트 코드를 제거하는 대표적인 예가 람다식이다.


## DI 라이브러리 종류

### Dagger2
- 구글에서 미는 라이브러리
- 러닝커브 높음
- 추적 가능한 보일러 플레이트 코드를 컴파일 시간에 자동으로 생성

### Koin
- Dagger보다 낮은 러닝커브
- 코틀린으로 작성되어 코틀린과 호환 좋음
- MVVM 패턴 만들기 용이



# Koin

## Koin 단계
1.  `모듈`  생성하기 (Koin DSL; Domain Specific Language)
2.  `Android Application Class`에서  `startKoin()`으로 실행하기
3.  의존성 주입

## Koin DSL
- `module` :   : Koin 모듈 생성
-   `factory`  : inject 하는 시점에 인스턴스 생성
-   `single`  : 싱글톤 생성, 앱이 살아있는 동안 전역적으로 사용가능
-   `bind`  : 생성할 객체를 다른 타입으로 바인딩할 때 사용
-   `get`  : 컴포넌트내에서 알맞은 의존성을 주입함





# Dagger2

## Dagger2의 컴포넌트



<br><br><br>
> :bookmark: __REFERENCE__ <br>
> https://velog.io/@jojo_devstory/DIDependency-Injection%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90<br>
> https://jungwoon.github.io/android/2019/08/21/Koin/<br>
> 
