# Repository Pattern



## 발생 배경

비즈니스 로직은 보통 데이터베이스, 웹서비스 등의 데이터 저장소에 접근하지만, 여러 문제를 야기할 수 있다.

ex) 

- 중복 코드
- 잠재적 오류
- 오타
- 외부 의존성과 격리되어 비즈니스 로직을 쉽게 테스트할 수 없음? (An inability to easily test the business logic in isolation from external dependencies)



## 목표

- 데이터 레이어를 분리
- 데이터와 서비스 접근 로직에서 비즈니스 로직을 분리하여 유지보수와 가독성 향상
- 한 데이터 소스에 여러개가 접근한다면, 일관된 데이터와 로직을 제공하고 중앙 집중처리를 지원하고 싶음



## 솔루션 -> Repository

- 레포지토리는 데이터 소스 레이어와 비즈니스 레이어 사이를 중재
- 레포지토리는 쿼리를 날리거나, 데이터를 새롭게 mapping함

![image](https://developer.android.com/topic/libraries/architecture/images/final-architecture.png?hl=ko)

## 개념

- 데이터가 있는 여러 저장소 (Local, Remote)를 추상화하여 중앙 집중 처리 방식 구현
- 데이터를 사용하는 Domain(ex. Viewmodel)에서는 비즈니스 로직에만 집중할 수 있다 
  + 데이터의 출처는 몰라도됨
  + 데이터가 로컬 DB에서 가져오는지, API 응답을 통해 가져오는지 ViewModel은 알 필요 없다!
  + ViewModel이 여러 Repository를 공유하여 데이터의 일관성 유지 가능
- Repository가 추상화되어 있으므로 항상 같은 interface로 데이터 요청 가능



## 장점

- 데이터 로직 분리 가능
- 중앙 집중 처리 방식 --> 일관된 인터페이스로 데이터 요청 가능
- 어떤 데이터를 가져올지는 repository에서 결정하여 데이터 제공
- 단위 테스트를 통한 검증 가능
- 데이터 저장소에 있는 데이터를 캡슐화 --> **객체지향적**
- 객체 간의 결합도 감소
- 어플리케이션의 전체적인 디자인이 진화해도 적용할 수 있는 유연한 아키텍쳐 제공









> :bookmark: **REFERENCE**<br>
>
> [Repository Pattern 이해하기](https://0391kjy.tistory.com/39)<br>
>
> [[Design Pattern\] Repository패턴이란](https://eunjin3786.tistory.com/198)<br>
>
> [The Repository Pattern](https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff649690(v=pandp.10)?redirectedfrom=MSDN)<br>
>
> [The “Real” Repository Pattern in Android](https://proandroiddev.com/the-real-repository-pattern-in-android-efba8662b754)<br>



