# 01. 100만 달러짜리 빠른 앱을 만드는 비법 전수



## View 성능 높이기

### 1. 오버드로우 줄이기 

- 중첩된 배경 제거
- 투명도 사용 삼가 : 부가적인 연산 필요

### 2 View의 간소화 및 갱신 빈도 낮추기

- onDraw는 수시로 할당될 수 있음. onDraw에서 메모리를 할당하거나 초기화하는 작업
- invalidate, requestLayout 삼가. CPU나 GPU에 부담됨
- onDraw, onMeasure, onLayout이 자주 호출되지 않도록 한다

### 3 ConstraintLayout 사용하기

- 레이아웃 계층이 많을수록 View를 순회하는 과정이 깊다
- ConstraintLayout은 계층을 평탄화하므로 비교적 빠르다

### 4. ViewStub 사용으로 느리게 초기화

- 복잡하게 구성된 레이아웃을 빠르게 전개시켜야하는 상황에서, ViewStub을 사용해 레이아웃의 전개 시기를 선택적으로 늦출수 있다. 사용자가  스크롤할 때 view하나가 상당한 시간이 걸리면 버벅이게 보임. 사용자가 빠르게 스크롤할수있도록 불필요한 레이아웃의 전개를 제어하고 전개의 시기를 늦추는 방법으로 성능을 개선할 수 있음

### 5. RecyclerView 퍼포먼스 향상

- 아이템 갱신 최소화하기 : 특정 아이템만 갱신
- DiffUtil 사용하기 : 두 리스트의 차이를 계산하고 변경된 부분만 갱신하도록 도와줌
- setHasFixedSize(true) 호출 : 어댑터에 아이템이 추가/제거될 때마다 recyclerview의 크기가 변경되는지를 건너뛸수있음
- setItemViewCacheSize(int) 호출 : 아이템 view가 pool로 들어가기 전에 유지되는 캐시의 사이즈를 결정함
- setRecycledViewPool(RecyclerVIewPool) 호출: recyclerview간의 view pool을 공유해 성능을 개선함 
- setHasStableIds(true) : 이미 bind된 아이템에 대해 onBindViewHolder 호출을 방지해 성능을 개선함



## 앱 성능을 개선하기 위한 도구

### Layout Inspector

- 레이아웃의 세부 정보를 검토할 때 사용

### 프로파일러

- 앱의 CPU, 메모리, 네트워크 사용량 등을 검사

### Lint

- 정적 코드 스캔 도구

### GPU 렌더링 속도 프로파일링

- 개발자옵션 -> 모니터링 섹션에서 활성화

### GPU 오버드로우 시각화

- GPU 오버드로우 디버그 옵션 활성화



https://tv.naver.com/v/15353556/list/629240