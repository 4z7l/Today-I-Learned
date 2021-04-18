# CPU 스케줄링 - (2)

CPU 스케줄링 알고리즘



## 선점 스케줄링

### FCFS(First Come First Served)

- 비선점
- 먼저온거 먼저 처리, 큐에 도착한 순서대로
- Convoy Effect : 짧은 process가 오래 기다려야 하는 경우

<br>

### SJF(Shortest Job First)

- 비선점/선점 버전 있음. 선점 버전은 SRTF(Shortest Remaining Time First)
- Optimal. 가장 짧은 대기시간을 보장함
- 수행시간이 가장 짧은 작업 먼저 수행
- starvation 발생시킬수있음.  긴 작업은 영원히 CPU를 할당받지 못할 수도 있음

<br>

## 비선점 스케줄링

### Priority Scheduling

- 우선순위가 높은 프로세스에게 CPU 할당
- SJF는 일종의 Priority Scheduling
- Starvation 발생 가능. 낮은 우선순위는 영원히 CPU 할당받지 못할 수도.
- -> Aging을 통해 해결가능

<br>

### Round Robin

- 각 프로세스는 동일한 크기의 할당 시간(Time Quantum)을 가짐
- 할당 시간이 지나면 선점 당하고 레디큐 제일 뒤로 감
- 짧은 작업, 긴 작업이 섞여있을 때 효율적
- q Time Unit 이 작으면 : Context Switch 오버헤드 커짐 / 크면 : FCFS

<br>

### Multilevel-Queue

- Ready Queue를 여러 개로 분할

- foreground : interactive한 작업, RR 사용

- background : batch- no human interaction, FCFS 사용

  

<br>

### Multilevel-Feedback-Queue

- 프로세스가 다른 큐로 이동 가능
- Aging과 같은 방식으로 구현 가능