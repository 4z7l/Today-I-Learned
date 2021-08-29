# 안드로이드의 메모리 관리 방식



- 안드로이드 런타임(ART)와 Dalvik 가상 머신은 페이징과 메모리 매핑을 통해 메모리를 관리함



### 가비지 컬렉션

- 가비지 컬렉션 : 사용하지 않는 메모리를 회수하는 것
- 가장 최근에 할당됨 -> young generation
- 오래 활성 상태 -> old generation -> permanent generation



### 메모리 공유

- 앱 프로세스는 Zygote 프로세스에서 fork됨
- Zygote 프로세스 : 시스템이 부팅되고 일반 프레임워크 코드나 리소스가 로드될 때 시작됨
- 시스템은 Zygote 프로세스를 fork하고 새로운 프로세스의 코드를 로드하고 실행함



### 앱 전환

- 앱을 전환하면 포그라운드 상태가 아닌 앱이나 포그라운드 서비스를 실행하지 않는 앱을 캐시에 보관함.
- 메모리같은 자원이 부족해지면 시스템은 캐시에 있는 프로세스를 종료함



### 메모리 할당

- 안드로이드는 기본적으로 free memory는 메모리 낭비라고 생각함. 가능한 모든 메모리를 사용하려고 함

![img](https://developer.android.com/images/games/memory-types.svg)



### 메모리 페이지

- RAM은 4KB의 page로 나뉨
- 페이지는 카테고리가 있음
  1. cached : 저장소의 파일로 지원
     - private : 하나의 프로세스에서 소유
     - shared : 여러 프로세스에서 사용
  2. anonymous : 저장소의 파일로 지원하지 않음



### 메모리 부족 관리

#### 커널 스왑 데몬 (kswapd)

- 사용된 메모리를 가용 메모리로 변환함
- demand paging 기법



#### 로우 메모리 킬러(LMK)

- 실행중인 프로세스의 우선순위를 정하고 높은 것들 먼저 종료
- 백그라운드 앱 -> 시스템 프로세스 순서로 종료

![](https://developer.android.com/images/games/lmk-process-order.svg?hl=ko)



https://developer.android.com/topic/performance/memory-overview