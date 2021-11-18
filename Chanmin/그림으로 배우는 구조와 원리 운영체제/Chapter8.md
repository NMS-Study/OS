# 08 가상메모리

### 메모리(기억장치)의 종류


### Virtual Storage (Memory)

    - Non-continuous allocation
    - 사용자 프로그램을 여러 개의 block으로 분할
    - 실행 시, 필요한 block들만 메모리에 적재
        - 나머지 block 들은 swap device에 존재
    - 기법들
        - Paging system
        - Segmentation system
        - Hybrid paging, segmentation system

### Non-continuous allocation

    - Virtual address(가상주소) = relative address
        - Logical address(논리주소)
            - 연속된 메모리 할당을 가정한 주소 
        - Real address(실제주소) = absolute(physical)
            - 실제 메모리에 적재된 주소
    - Address mapping
        - Virtual address를 real address로 바꾸는 것을 말함


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-1.jpg" alt="그림 8-1" style="border:1px; border-style: solid; zoom:100%;"/>

    - 장점 : 사용자/프로세스는 실행 프로그램 전체가 메모리에 연속적으로 적재되었다고 가정하고 실행 할 수 있음

### Block Mapping

    - 사용자 프로그램을 block 단위로 분할 및 관리
        - 각 block에 대한 address mapping 정보 유지
    - Virtual address : v = (b, d)
        - b = block number
        - d = displacement(offset) in a block

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-2.jpg" alt="그림 8-2" style="border:1px; border-style: solid; zoom:100%;"/>

    - Block map table(BMT)
        - Address mapping 정보 관리
            - kernel 공간에 프로세스마다 하나의 BMT를 가짐

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-3.jpg" alt="그림 8-3" style="border:1px; border-style: solid; zoom:100%;"/>

        - Residence bit : 해당 블록이 메모리에 적재되었는지 여부 (0 또는 1)

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-4.jpg" alt="그림 8-4" style="border:1px; border-style: solid; zoom:100%;"/>

    - Block Mapping의 흐름
        - 1. 프로세스의 BMT에 접근
        - 2. BMT에서 block b에 대한 항목(entry)를 찾음
        - 3. Residence bit 검사
            - 3.1. Residence bit = 0 경우,
                - swap device에서 해당 블록을 메모리로 가져옴
                - BTM 업데이트 후 3.2. 단계 수행
            - 3.2. Residence bit = 1 경우,
                - BMT에서 b에 대한 real address 값 a 확인
        - 4. 실제 주소 r 계산(r = a + d)
        - 5. r을 이용하여 메모리에 접근


### Virtual Storage Methods

    - Paging system
    - Segmentation system
    - Hybird paging/segmentation system


### Paging System

    - 프로그램을 같은 크기의 블록으로 분할(Pages)
        - pages : 같은 크기의 블록

    - Terminologies
        - Page
            - 프로그램의 분활된 block
    
        - Page frame
            - 메모리의 분할 영역
            - Page와 같은 크기로 분할

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-5.jpg" alt="그림 8-5" style="border:1px; border-style: solid; zoom:100%;"/>

    - 특징
        - 논리적 분할이 아님 (크기에 따른 분할)
            - Page 공유(Sharing) 및 보호(Protection) 과정이 복잡함
                - Segmentation 대비

        - Simple and Efficient
            - Segmentation 대비

        - No external fragmentation (외부 단편화 없음)
            - Internal fragmentation 발생 가능

    - Address Mapping (Block Mapping과 비슷)

        - Virtual address : v = (p,d)
            - p : page number
            - d : displacement(offset)

        - Address mapping
            - PMT(Page Map Table) 사용
                - block mapping에서는 BMT

        - Address mapping mechanism
            - Direct mapping (직접 사상)
                - block mapping과 유사
            - Associative mapping (연관 사상)
                - TLB(Translation Look-aside Buffer)
            - Hybrid direct/associative mapping


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-6.jpg" alt="그림 8-6" style="border:1px; border-style: solid; zoom:100%;"/>

- residence bit : 올라갔는지 안올라갔는지
- page frame number : 어디에 올라가 있는지
- secondary storage address : 스왑 디바이스 어디에 올라가 있는지 확인

<br>

        - Direct mapping
            - Block mapping 방법과 유사
            - 가정
                - PMT를 커널 안에 저장되어있다
                - PMT entry size => entrySize 변수로 지정
                - Page size => pageSize 변수로 지정


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-7.jpg" alt="그림 8-7" style="border:1px; border-style: solid; zoom:100%;"/>


        - Direct Mapping의 흐름
            - 1. 해당 프로세스의 PMT가 저장되어 있는 주소 b에 접근
            - 2. 해당 PMT에서 page p에 대한 entry 찾음
                - p의 entry 위치 = b + p * entrySize
            - 3. 찾아진 entry의 존재 비트 검사
                - 3.1. Residence bit = 0인 경우 (page fault: 페이지를 찾는데 실패했다)
                    - swap device에서 해당 page를 메모리로 적재
                    - PMT를 갱신한 후 3.2. 단계 수행
                - 3.2. Residence bit = 1인 경우
                    - 해당 entry에서 page frame 번호 p'를 확인
            - 4. p'와 가상 주소의 변위 d를 사용하여 실제 주소 r 형성
                - r = p' * pageSize + b
            - 5. 실제 주소 r로 주기억장치에 접근

        - 문제점
            - 메모리 접근 횟수가 2배
                - 성능 저하 발생
            - PMT를 위한 메모리 공간 필요

        - 해결 방안
            - Associative mapping (TLB)
            - PMT를 위한 전용 기억장치(공간) 사용
                - Dedicated register or cache memory
            - Hierarchical paging
            - Hashed page table
            - Inverted page table


        - Associative Mapping
            - TLB(Translation Look-aside Buffer)에 PMT 적재
                - Associative high-speed memory
                    - PMT 전용 메모리
            - PMT를 병렬 탐색
            - Low overhead, high speed
            - Expensive hardware (근데 겁나 비쌈, 그래서 겁나 작음)
                - 큰 PMT를 다룰 수 없음
                    - 따라서 하이브리드 다이랙트 방법 생김
            

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-8.jpg" alt="그림 8-8" style="border:1px; border-style: solid; zoom:100%;"/>


        - Hybrid Direct/Associative Mapping
            - 두 기법을 혼합하여 사용
                - HW 비용은 줄이고, Associative mapping의 장점 활용

            - 작은 크기의 TLB 사용
                - PMT : 메모리(커널 공간)에 저장
                - TLB : PMT 중 일부 entry들을 적재
                    - 최근에 사용된 page들에 대한  entry 저장
                    - Locality (지역성) 활용
                        - 프로그램의 수행과정에서 한 번 접근한 영역을 다시 접근(temporal locality)
                        - 또는 인접 영역을 다시 접근(spatial locality)할 가능성이 높음


        - Hybrid Direct/Associative Mapping 흐름

            - 프로세스의 PMT가 TLB에 적재되어 있는지 확인
                - 1. TLB에 적재되어 있는 경우
                    - residence bit를 검사하고 page frame 번호 확인\
                - 2. TLB치에 적재되어 있지 않은 경우
                    - Direct mapping으로 page frame 번호 확인
                    - 해당 PMT entry를 TLB에 적재

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-9.jpg" alt="그림 8-9" style="border:1px; border-style: solid; zoom:100%;"/>


### Memory Management

    - Page와 같은 크기로 미리 분할하여 관리/사용
        - Page frame
        - FPM 기법과 유사

    - Frame table
        - Page frame당 하나의 entry
        - 구성
            - Allocated/available field
            - PID field
            - Link field : For free list (사용가능 한 fp들을 연결)
            - AV : Free list header (free list의 시작점)


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-10.jpg" alt="그림 8-10" style="border:1px; border-style: solid; zoom:100%;"/>


### Page Sharing

    - 여러 프로세스가 특정 page를 공유 가능
        - Non-continuous allocation!

    - 공유 가능 page
        - Procedure pages
            - Pure code(reenter code: 재진입코드, 함수 내부로 다시 진입)

        - Data page
            - Read-only data
            - Read-write data
                - 병행성(concurrency) 제어 기법 관리하에서만 가능

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-11.jpg" alt="그림 8-11" style="border:1px; border-style: solid; zoom:100%;"/>

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-12.jpg" alt="그림 8-12" style="border:1px; border-style: solid; zoom:100%;"/>


    - Procedure Page Sharing의 문제와 해결법

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-13.jpg" alt="그림 8-13" style="border:1px; border-style: solid; zoom:100%;"/>

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-14.jpg" alt="그림 8-14" style="border:1px; border-style: solid; zoom:100%;"/>


### Page Protection

    - 여러 프로세스가 page를 공유할 때
        - Protection bit 사용


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-15.jpg" alt="그림 8-15" style="border:1px; border-style: solid; zoom:100%;"/>


### Paging System - Summary

    - 프로그램을 고정된 크기의 block으로 분할(page)
    - 메모리를 block size로 미리 분할 (page frame)
        - 외부 단편화 문제 없음
        - 내부 단편화는 발생
        - 메모리 통합/압축 불필요
        - 프로그램의 논리적 구조 고려하지 않음
            - Page sharing/protection이 복잡

    - 필요한 page만 page frame에 적재하여 사용
        - 메모리의 효율적 활용

    - Page mapping overhead
        - 메모리 공간 및 추가적인 메모리 접근이 필요
        - 전용 HW활용(TLB)으로 해결 가능
            - 그러나 하드웨어 비용이 증가


### Segmentation System

    - 프로그램을 논리적 block으로 분할 (Segment)
        - Block의 크기가 서로 다를 수 있음
        - 예) stack, heap, main procedure, shared lib, Etc

    - 특징
        - 메모리를 미리 분할 하지 않음
            - VPM과 유사

        - Segment sharing/protection이 용이 함
        - Address mapping 및 메모리 관리의 overhead가 큼
        - No internal fragmentation
            - External fragmentation 발생 가능

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-16.jpg" alt="그림 8-16" style="border:1px; border-style: solid; zoom:100%;"/>

    - Address mapping
        - Virtual address: v=(s,d)
            - s: segment number
            - d: displacement in a segment

        - Segment Map Table (SMT)
        - Address mapping mechanism
            - Paging system과 유사


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-17.jpg" alt="그림 8-17" style="border:1px; border-style: solid; zoom:100%;"/>

segment length : 크기
<br>
protection bits : 접근 권한을 나눌 수 있음


    - Address mapping (direct mapping)

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-18.jpg" alt="그림 8-18" style="border:1px; border-style: solid; zoom:100%;"/>


    - Address mapping (direct mapping)의 흐름
        - 1. 프로세서의 SMT가 저장되어 있는 주소 b에 접근
        - 2. SMT에서 segment s의 entry 찾음
            - s의 entry 위치 = b + s * entrySize
        - 3. 찾아진 Entry에 대해 다음 단계들을 순차적으로 실행
            - 3.1. 존재 비트가 0 인 경우,
                - // missing segment fault
                - swap deive로 부터 해당 segment를 메모리로 적재 SMT를 갱신
            - 3.2. 변위(d)가 segment 길이보다 큰 경우 (d > ls),
                - segment overflow exception 처리 모듈을 호출
            - 3.3. 허가되지 않은 연산일 경우 (protection bit field 검사),
                - segment protection exception 처리 모듈을 호출
        - 4. 실제 주소 r 계산 (r = as + d)
        - 5. r로 메모리에 접근


    - Memory management
        - VPM과 유사
            - Segment 적재 시, 크기에 맞추어 분할 후 적재


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-19.jpg" alt="그림 8-19" style="border:1px; border-style: solid; zoom:100%;"/>


    - Segment sharing / protection
        - 논리적으로 분할되어 있어, 공유 및 보호가 용이함


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-20.jpg" alt="그림 8-20" style="border:1px; border-style: solid; zoom:100%;"/>


    - Summary
        - 프로그램을 논리 단위로 분할 (segment)
        - 메모리를 동적으로 분할
            - 내부 단편화 문제 없음
            - Segment sharing/protextion이 용이함
            - Paging system 대비 관리 overhead가 큼
        - 필요한 segment만 메모리에 적재하여 사용
            - 메모리의 효율적 활용
        - Segment mapping overhead
            - 메모리 공간 및 추가적인 메모리 접근이 필요
            - 전용 HW 활용으로 해결 가능

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-21.jpg" alt="그림 8-21" style="border:1px; border-style: solid; zoom:100%;"/>


### Hybrid Paging / Segmentation

    - Paging과 Segmentation의 장점 결합
    
    - 프로그램 분할
        - 1. 논리 단위의 segment로 분할
        - 2. 각 segment를 고정된 크기의 page들로 분할

    - Page단위로 메모리에 적재

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-22.jpg" alt="그림 8-22" style="border:1px; border-style: solid; zoom:100%;"/>


    - Address mapping
        - Virtual address : v = (s, p, d)
            - s : segment number
            - p : page number
            - d : offset in a page

        - SMT와 PMT 모두 사용
            - 각 프로세스 마다 하나의 SMT
            - 각 segment마다 하나의 PMT

        - Address mapping
            - Direct, associated 등
        
        - 메모리 관리
            - FPM과 유사


<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-23.jpg" alt="그림 8-23" style="border:1px; border-style: solid; zoom:100%;"/>

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-24.jpg" alt="그림 8-24" style="border:1px; border-style: solid; zoom:100%;"/>

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-25.jpg" alt="그림 8-25" style="border:1px; border-style: solid; zoom:100%;"/>

<img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter8\그림 8-26.jpg" alt="그림 8-26" style="border:1px; border-style: solid; zoom:100%;"/>


    - Summary
        - 논리적 분할(segment)와 고정 크기 분할(page)을 결합
            - Page sharing/protection이 쉬움
            - 메모리 할당/관리 overhead가 작음
            - No external fragmentation

        - 전체 테이블의 수 증가
            - 메모리 소모가 큼
            - Address mapping 과정이 복잡

        - Direct mapping의 경우, 메모리 접근이 3배
            - 성능이 저하될 수 있음


