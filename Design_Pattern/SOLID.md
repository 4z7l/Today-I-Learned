## 애플리케이션 설계

- 아주 중요하다.
- 앱은 구현하고 나면 변경 시 많은 비용 소요
- 잘 설계된 애플리케이션은 유지보수와 성능 보안 안정성에 많은 이점
- 따라서 처음 애플리케이션을 제대로 설계하는게 아주 중요

## SOLID 원칙

- 로버트 C. 마틴이 객체 지향 프로그래밍 및 설계에 대해 소개한 5가지 원칙이다
- 각 원칙의 앞글자를 따서 SOLID라고 부른다
- 가독성 높이고 확장 쉬운 구조 만드는 지침



### **SRP**) The Single Responsibility Principle.

- 단일 책임 원칙
- 클래스는 하나의 책임만 가짐
- 클래스나 모듈은 분리하여 단 하나의 기능을 가져야함
- 변경 사항이 생겨도 그 부분만 수정하면됨
- 관심사를 분리해야함
- GUI 코드랑 비즈니스 로직을 같이 두면 안됨

> *Gather together the things that change for the same reasons. Separate things that change for different reasons.*



### **OCP**) The Open-Closed Principle.

- 개방 폐쇄 원칙
- 확장에 대해선 열리고, 수정에 대해선 닫혀야함
- 어떤 내용 수정하기 위해 다른 코드나 모듈까지 수정하는건 힘듦
- 객체 지향 프로그래밍에서 지켜야할 기본적인 핵심 원칙
- 이 원칙 무시하면 객체 지향 프로그래밍 장점인 유연성,재사용성,유지보수성 획득 불가
- 추상적인개념과 구체적 개념 분리 / GUI와 비즈니스 룰 분리 등...

> *A Module should be open for extension but closed for modification.*



### **LSP**) The Liskov Substitution Principle.

- 리스코프 치환 원칙
- 클래스 B가 A의 자식이라면 A를 B로 치환할수 있어야함
- = 다운캐스팅이 문제 없어야함
- 추상화를 잘해야한다. 

```
class A {}
class B extends B {}
class C extends C {}
```

- List<? extends B> list 는 List<C>사용 가능 List<A>도 사용가능

> *A program that uses an interface must not be confused by an implementation of that interface.*



### **ISP**) The Interface Segregation Principle.

- 인터페이스 분리 원칙
- 클래스는 자신이 사용하지 않는 메소드에 의존하고있으면 안됨
- 만약 사용하지 않는 메소드가 바뀌면 그 client도 다시 빌드하고 다시 deploy해야함
- 인터페이스르 구체적이고 작은 단위로 분리해야함

> *Keep interfaces small so that users don’t end up depending on things they don’t need.*





### **DIP**) The Dependency Inversion Principle.

- 의존 역전 원칙
- 상위 계층이 하위 계층의 구현으로부터 독립되게 함
- 1) 상위 모듈은 하위 모듈에 의존하면 안됨, 모두 추상화에 의존해야함
- 2) 추상화는 세부사헝에 의존하면 안됨, 세부사항이 추상화에 의존해야함
- 

> *Depend in the direction of abstraction. High level modules should not depend upon low level details.*



> :bookmark: **REFERENCE**<br>
>
> http://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html<br>
>
> 