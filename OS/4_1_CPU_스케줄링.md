# CPU 스케줄링 - (1)



### CPU 스케줄러 & 디스패처

#### Scheduler

- Ready 상태의 프로세스 중에서 어떤 프로세스에게 CPU를 줄 지 고름

### Dispatcher

- CPU 제어권을 선택된 프로세스에게 넘김
- 이 과정을 Context Switch라 함

<br>

#### CPU 스케줄링 필요한 경우

1. Running -> Blocked (I/O 요청 시)
2. Running -> Ready (할당 시간 만료로 Timer Interrupt)
3. Blocked -> Ready
4. Terminate

1,4 -> nonpreemptive (비선점, 자진 반납)<br>

2,3, -> preemptive (선점, 강제로 빼앗음)



<br>

### Scheduling Criteria (성능 척도)

- CPU Utilization(이용률) : 전체 시간 중 CPU가 놀지 않고 일한 시간, 이용률이 높을수록 좋음
- Throughput(처리량) : 단위 시간당 처리량, CPU가 얼마나 많은 일을 했는가, 높을수록 좋음
- Turnaround Time(소요시간, 반환시간) : CPU 사용한 시간 + 기다린 시간, 짧을수록 좋음
- Waiting Time(대기시간) : 프로세스가 Ready Queue에서 기다린 전체 시간의 합, 짧을수록 좋음
- Response Time(응답시간) : 프로세스가 Ready Queue에 들어가서 최초로 CPU 얻기까지의 시간, 짧을수록 좋음