# 07 메모리 관리

### 메모리(기억장치)의 종류

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-1.jpg" alt="그림 7-1" style="border:1px; border-style: solid; zoom:100%;"/>

- 운영체제가 다루는 메모리는 4가지 종류가 존재

    - 레지스터, 캐시, 메인 메모리, 보조기억장치

    - 위로 갈수록 속도와 가격이 오르고 아래로 갈수록 용량이 낮아짐

레지스터와 캐시는 HW가 관리

    - 즉 CPU가 관리

- 메인 메모리와 보조 기억장치는 SW가 관리

    - 즉 OS가 관리

### 메모리(기억장치) 계층구조

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-2.jpg" alt="그림 7-2" style="border:1px; border-style: solid; zoom:100%;"/>

- 보조기억장치(HDD, SSD)에서 1bit를 메인 메모리로 읽으려면(가져오려면) 얼마만큼 읽을 수 있을까

    - 그 최소 단위는 Block으로 Size는 1 ~ 4KB

    - Block은 보조기억장치와 주기억장치 사이의 데이터 전송 단위

- 메인 메모리에서 CPU 안에 레지스터로 보내는 단위는 Word

    - Word는 주기억장치와 레지스터 사이의 데이터 전송 단위
    - Size: 16 ~ 64bits
    - CPU가 32bit인지 64bit인지를 결정하는 요소


### Address Binding

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-3.jpg" alt="그림 7-3" style="border:1px; border-style: solid; zoom:100%;"/>

- "주소를 묶는다"

    - 프로그램의 논리 주소를 실제 메모리의 물리 주소로 매핑(mapping) 하는 작업을 뜻함

    - 즉, int a; -> 메모리 상에 해당 변수가 있게 끔 연동해주는 작업

- Binding 시점에 따른 구분(언제 이 주소를 매핑하느냐)

    - Compile time binding
    - Load time binding
    - Run time binding



<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-4.jpg" alt="그림 7-4" style="border:1px; border-style: solid; zoom:100%;"/>

- 위 그림은 소스 코드를 짜고 실행되기까지의 과정

    - Compiler : 소스 코드를 짜고 컴파일을 함 -> Compile time binding
        - 이를 Compile time이라고 함
    - Linker : 오브젝트 모듈을 만든 다음에는 다른 라이브러리를 가져다 썼으면 이 모듈과 묶어서 실행 가능한 형태의 로드 모듈로 만드는 과정을 진행
    - Loader : 실행 파일이 만들어지고 더블 클릭 등의 모션으로 메모리에 올라가도록 로드 모뮬을 메모리에 올려주는 역할을 함
        - Linker부터 Loader까지의 과정을 Load time이라고 함

    - 로더를 통해서 우리의 프로세스가 메모리에 올라가면은 메모리 안에서 실행이 됨
    - 실행되는 중에 주소를 정해주는 걸 Run time binding
        - 이를 Run time이라고 함


- Compile time binding
    - 프로세스가 메모리에 적재될 위치를 컴파일러가 알 수 있는 경우
        - 위치기 변하지 않음
    - 프로그램 전체가 메모리에 올라가야 함

- Load time binding
    - 메모리 적재 위치를 컴파일 시점에서 모르면, 대체 가능한 상대 주소를 생성
    - 적재 시점(load time)에 시작 주소를 반영하여 사용자 코드 상의 주소를 재설정
    - 프로그램 전체가 메모리에 올라가야 함

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-5.jpg" alt="그림 7-5" style="border:1px; border-style: solid; zoom:100%;"/>

- Run-time binding
    - Address binding을 수행시간(ready->run)까지 연기
        - 프로세스가 수행 도중 다른 메모리 위치로 이동할 수 있음
    - HW의 도움이 필요
        - MMU : Memory Management Unit
    - 대부분의 OS가 사용

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-6.jpg" alt="그림 7-6" style="border:1px; border-style: solid; zoom:100%;"/>

### Dynamic Loading

- 모든 루틴(function A~Z)을 교체 가능한 형태로 디스크에 저장

- 실제 호출 전까지는 루틴을 적재하지 않음
    - 메인 프로그램만 메모리에 적재하여 수행(function A만)
    - 루틴의 호출 시점에 address binding 수행

- 장점
    - 메모리 공간의 효율적 사용


### Swapping

- 프로세서 할당이 끝나고 수행 완료 된 프로세스는 swap-device로 보내고 (Swap-out)

- 새롭게 시작하는 프로세스는 메모리에 적재(Swap-in)

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-7.jpg" alt="그림 7-7" style="border:1px; border-style: solid; zoom:100%;"/>


### Memory Allocation

- 메모리를 프로세스에게 어떻게 할당해 주는가

### Continuous Memory Allocation

- 정의 : 프로세스(context)를 하나의 연속된 메모리에 공간에 할당하는 정책
    - 프로그램, 데이터, 스택 등
- 메모리 구성 정책
    - 메모리에 동시에 올라갈 수 있는 프로세스 수
        - Multiprogramming degree
    - 각 프로세스에게 할당되는 메모리 공간 크기
    - 메모리 분할 방법

- Uni-programming
    - Multiprogramming degree = 1
        - 멀티 프로세스가 한번에 하나만 올라갈 수 있음

    - 하나의 프로세스만 메모리 상에 존재
    - 가장 간단한 메모리 관리 기법

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-8.jpg" alt="그림 7-8" style="border:1px; border-style: solid; zoom:100%;"/>

    - 문제점 1
        - 프로그램의 크기가 메모리 크기 보다 클 경우
        - 프로그램 크기 > 메모리 크기
        - 프로그램을 잘라야함

    - 해결법 1
        - Overlay structure
            - 메모리에 현재 필요한 영역만 적재
            - 사용자가 프로그램의 흐름 및 자료구조를 모두 알고 있어야 함

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-9.jpg" alt="그림 7-9" style="border:1px; border-style: solid; zoom:100%;"/>

    - 문제점 2
        - 커널(Kernel) 보호
        - 프로그램을 올릴 때 커널을 침범해서 올리게 되면은 프로그램이 죽음

    - 해결법 2
        - 경계 레지스터 (boundary register) 사용
        - 경계가 되는 지점에 주소를 적어줌으로써 넘어가지 않도록 할 수 있음

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-10.jpg" alt="그림 7-10" style="border:1px; border-style: solid; zoom:100%;"/>

    - 문제점 3
        - 원인 : 하나의 프로그램만 적재되니 나머지 공간이 낭비가 됨
        - Low system resource utilization (활용도가 낮음)
        - Low system performance (성능이 낮음)

    - 해결법 3
        - Multi-programming
        - 시스템에 여러가지 프로그램이 올라가면 됨


- Multi-programming

    - Fixed Partition Multiprogramming
        - 메모리 공간을 고정된 크기로 분할
            - 미리 분할되어 있음
            - 크기와 갯수를 정해 미리 분할
        - 각 프로세스는 하나의 partition(분할)에 적재
            - 어떤 프로세스가 도착한다면 적당한 공간에 넣어주기만 하면 됨
            - Process : Partition = 1 : 1
                - 한 파티션에는 하나의 프로세스 만
        - Partition의 수 = K
            - Multiprogramming degree = K

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-11.jpg" alt="그림 7-11" style="border:1px; border-style: solid; zoom:100%;"/>

- 자료구조 예

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-12.jpg" alt="그림 7-12" style="border:1px; border-style: solid; zoom:100%;"/>

- 커널 및 사용자 영역 보호
    - Uni programming처럼 커널이 침범되는 문제를 방지해야함
    - 경계마다 Boundary address를 배치

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-13.jpg" alt="그림 7-13" style="border:1px; border-style: solid; zoom:100%;"/>

- Fragmentation (단편화)

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-14.jpg" alt="그림 7-14" style="border:1px; border-style: solid; zoom:100%;"/>

    - Internal fragmentation
        - 파티션에 프로세스가 들어갔는데 남은 자투리 공간을 뜻함
        - 내부 단편화
        - Partition 크기 > Process 크기
            - 메모리가 낭비 됨

    - External fragmentation
        - 메모리 공간은 충분한데 파티션이 연속되지 않아서, 방이 없어서 들어가지 못하는 상황
        - 외부 단편화
        - (남은 메모리 크기 > Process 크기)지만, 연속된 공간이 아님
            - 메모리가 낭비됨

- Fixed Partition Multiprogramming 요약

    - 고정된 크기로 메모리 미리 분할
    - 메모리 관리가 간편함
        - Low overhead
    - 시스템 자원이 낭비 될 수 있음
    - Internal/external fragmentation


- Variable Partition Multiprogramming

    - 초기에는 전체가 하나의 영역

    - 프로세스를 처리하는 과정에서 메모리 공간이 동적으로 분할

    - No internal fragmentation

    - 배치 전략 (Placement strategies)

        - First-fit (최초 적합)
            - 충분한 크기를 가진 첫 번째 partition을 선택
            - Simple and low overhead
            - 공간 활용률이 떨어질 수 있음

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-15.jpg" alt="그림 7-15" style="border:1px; border-style: solid; zoom:100%;"/>

        - Best-fit (최적 적합)
            - Process가 들어갈 수 있는 partition 중 가장 작은 곳 선택
            - 탐색시간이 오래 걸림 (overhead 발생)
                - 모든  partition을 살펴봐야 함
            - 장점 : 크기가 큰 partition을 유지할 수 있음 
            - 단점 : 작은 크기의 partition이 많이 발생
                - 활용하기 너무 작은

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-16.jpg" alt="그림 7-16" style="border:1px; border-style: solid; zoom:100%;"/>

        - Worst-fit (최악 적합)
            - Process가 들어갈 수 있는 partition 중 가장 큰 곳 선택
            - 탐색시간이 오래 걸림
                - 모든 partition을 살펴봐야 함
            - 장점 : 작은 크기의 partition 발새을 줄일 수 있음
            - 단점 : 큰 크기의 partition 확보가 어려움
                - 큰 프로세스에게 필요한 공간이 없음

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-17.jpg" alt="그림 7-17" style="border:1px; border-style: solid; zoom:100%;"/>

        - Next-fit (순차 최초 적합)
            - 최초 적합 전략과 유사
            - State table에서 마지막으로 탐색한 위치부터 탐색
            - 메모리 영역의 사용 빈도 균등화
            - Low overhead

    - 어디에 배치할 것인가

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-18.jpg" alt="그림 7-18" style="border:1px; border-style: solid; zoom:100%;"/>

        - External fragmentation issue 발생

        - Coalescing holes (공간 통합)
            - 인접한 빈 영역을 하나의 partition으로 통합
                - Process가 memory를 release하고 나가면 수행
                - Low overhead

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-19.jpg" alt="그림 7-19" style="border:1px; border-style: solid; zoom:100%;"/>

        - Storage Compaction (메모리 압축)
            - 모든 빈 공간을 하나로 통합
            - 프로세스 처리에 필요한 적재 공간 확보가 필요할 때 수행
            - High overhead
                - 모든 Process 재배치 (Process 중지)
                - 많은 시스템 자원을 소비

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter7\그림 7-20.jpg" alt="그림 7-20" style="border:1px; border-style: solid; zoom:100%;"/>

- Continuous Memory Allocation 요약

    - Uni-programming
        - Simple
        - Fragmentation problem

    - Fixed partition multi-programming (FPM)
    - Variable partition multi-programming (VPM) 
        - Placement strategies
            - First-fit, Best-fit, Worst-fit, Next-fit
        - External fragmentation issue
            - Coalescing holes
            - Storage compaction