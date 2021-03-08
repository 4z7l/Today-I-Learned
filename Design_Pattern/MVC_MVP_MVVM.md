# MVC

### 개념

Model View Controller

- Model : 데이터와 데이터 처리
- View : 사용자에서 보여지는 데이터 UI
- Controller : 사용자의 입력을 받고 처리

### 동작

1. 사용자의 입력이 Controller에 들어옴
2. Controller는 입력 확인 후 Model 업데이트
3. Controller는 View에 Model 전달
4. View는 Model을 이용해 화면 보여줌

### 특징

- Controller는 여러개의 View를 선택할 수 있는 1:n구조, 직접 업데이트하지는 않음

### 장점

- 단순함

### 단점

- Model과 View 사이 의존성 높음
- 



# MVP

### 개념

- Model : 데이터와 데이터 처리하는 부분
- View : 사용자에게 보여지는 UI, 입력 받음
- Presenter : View에서 요청한 정보로 Model을 가공해 View에 전달
- Model과 View는 서로를 알 필요가 없음

### 동작

1. 사용자의 입력이 View에 들어옴
2. View는 데이터를 Presenter에 요청
3. Presenter는 Model에게 데이터 요청
4. Model은 Presenter에서 요청받은 데이터 응답
5. Presenter는 View에게 데이터 응답
6. View 업데이트

### 특징

- Presenter와 View는 1:1관계

### 장점

- MVC의 단점 해결 - Model과 View 사이 의존성 없음

### 단점

- View와 Presenter의 1:1의 의존성 증가



# MVVM

### 개념

- Model : 데이터와 데이터 처리하는 부분
- View : 사용자에게 보여지는 UI 부분
- ViewModel : View를 위한 Model, View를 나타내주기위한 Model이자 View를 나타내기위한 데이터 처리하는 부분

### 동작

1. 사용자의 입력이 View에 들어옴
2. View는 ViewModel에 입력 전달
3. ViewModel은 Model에 데이터 요청
4. Model은 ViewModel에 데이터 응답
5. ViewModel은 데이터 가공 및 저장
6. View는 ViewModel의 데이터를 통해 화면 나타냄(자동 갱신)

### 특징

- ViewModel과 View는 1:n
- 커맨드 패턴, 데이터바인딩 사용
- View에 입력이 들어오면 커맨드 패턴으로 ViewModel에 명령, Databinding으로 ViewModel의 값이 변하면 바로 View가 업데이트됨

### 장점

- View와 Model 사이 의존성 없음
- View와 ViewModel 사이의 의존성 없음
- 각 부분은 독립적이므로 모듈화하여 개발 가능

### 단점

- 구현 및 설계 어려움