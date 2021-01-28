# Memory

프로그램이 실행되려면 메모리에 적재(load)되어야 한다.

## 메모리의 구조

![img](http://tcpschool.com/lectures/img_c_memory_structure.png)

프로그램이 운영체제로부터 할당받는 메모리 공간 : 코드 영역, 데이터 영역, 힙 영역, 스택 영역
<br>
- 코드 영역 : 실행할 프로그램의 코드가 저장되는 공, 텍스트 영역이라고도 함
- 데이터 영역 : 전역 변수, 정적 변수 저장 / 프로그램 시작과 동시에 할당, 종료 시 소멸
- 힙 영역 : 사용자가 직접 관리하는 메모리 공간
- 스택 영역 : 함수의 호출과 동시에 할, 완료 시 소멸 / 스택 영역에 저장되는 함수의 정보를 스택 프레임(stack frame)이라 함



<br><br>
> :bookmark: **REFERENCE**<br>
[메모리의 구조](http://tcpschool.com/c/c_memory_structure)<br>
