# RxJava

## Backpressure와 Flowable

### Backpressure(배압)

- 데이터 생산과 소비가 불균형적인 경우 일어나는 현상
- 만약 데이터 발행은 1초마다, 소비는 10초마다 하면 소비와 관계없이 데이터는 계속 쌓임 --> OutOfMemoryError 발생
- 이런 현상을 배압이라 함


### Flowable

- 기존의 Observable은 배압 처리 불가
- 10000개 이상 데이터 처리하는 경우 Flowable 사용
-  스트림에 쌓이는 아이템의 양을 제어할 수 있는 해결책임

<br>

### Observable과 Flowable 선택 기준

#### Observable
- 1000개 미만 데이터 흐름
- OOME가 발생할 확률 적을때
- 마우스 이벤트, 터치 이벤트 등의 GUI 프로그래밍 -> Observable에서는 sample()이나 debounce()로 초당 1000회 이하 이벤트 핸들링 가능
- Observable은 Flowable보다 성능 오버헤드 낮음


#### Flowable
- 10000개 이상 데이터 처리
- 디스크에서 파일 읽을때, blocking/pull-based 방식이라 배압이랑 잘어울림?
- JDBC를 통해 DB 읽을때
- 네트워크 IO실행 시
- blocking/pull-based 방식을 사용하고 있는데 나중에 non blocking 방식의 reactive API 사용할 가능성 있는 경우


> ### When to use Observable
- You have a flow of no more than 1000 elements at its longest: i.e., you have so few elements over time that there is practically no chance for OOME in your application.
- You deal with GUI events such as mouse moves or touch events: these can rarely be backpressured reasonably and aren't that frequent. You may be able to handle an element frequency of 1000 Hz or less with Observable but consider using sampling/debouncing anyway.
- Your flow is essentially synchronous but your platform doesn't support Java Streams or you miss features from it. Using Observable has lower overhead in general than Flowable. (You could also consider IxJava which is optimized for Iterable flows supporting Java 6+).
> ### When to use Flowable
- Dealing with 10k+ of elements that are generated in some fashion somewhere and thus the chain can tell the source to limit the amount it generates.
- Reading (parsing) files from disk is inherently blocking and pull-based which works well with backpressure as you control, for example, how many lines you read from this for a specified request amount).
- Reading from a database through JDBC is also blocking and pull-based and is controlled by you by calling ResultSet.next() for likely each downstream request.
- Network (Streaming) IO where either the network helps or the protocol used supports requesting some logical amount.
- Many blocking and/or pull-based data sources which may eventually get a non-blocking reactive API/driver in the future.



<br>

### 배압 이슈에 대응하는 함수

- onBackpressureBuffer() : 배압 이슈가 발생했을 때 버퍼에 저장, 기본적으로 128개 버퍼 존재
- onBackpressureDrop() : 배압 이슈 발생 시 해당 데이터 무시
-  onBackpressureLatest() : 쌓이는 데이터 무시하면서 최신 데이터만 유지


<br>

### Room에서 비동기처리 시 반환값

![img](https://miro.medium.com/max/700/0*jEnmX0FZOBDdJIHK)

https://medium.com/androiddevelopers/room-flow-273acffe5b57



참고
https://stackoverflow.com/questions/40323307/observable-vs-flowable-rxjava2
https://github.com/ReactiveX/RxJava/wiki/What's-different-in-2.0#backpressure
