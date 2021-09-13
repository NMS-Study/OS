# 01 컴퓨터 하드웨어의 구성

- 컴퓨터 시스템은 데이터를 처리하는 물리적인 하드웨어와 어떤 작업을 지시하는 명령어로 작성한 프로그램인 소프트웨어로 구성됨

- 운영체제는 컴퓨터 하드웨어를 관리하는 소프트웨어

- 컴퓨터 하드웨어는 크게 프로세서, 메모리(기억장치), 주변장치로 구성됨
  - 이들은 시스템 버스로 연결되어있음

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-1 컴퓨터 하드웨어의 구성.jpg" alt="그림 1-1 컴퓨터 하드웨어의 구성" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-1 컴퓨터 하드웨어의 구성</figcaption>
</figure>





## 1. 프로세서

- 프로세서는 컴퓨터 하드웨어에 부착한 모든 장치의 동작을 제어하고 명령을 실행함
  - 중앙처리장치(CPU: Central Processing Unit)라고도 함
- 연산장치와 제어장치, 레지스터로 구성
  - 이들은 내부 버스로 연결됨

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-2 프로세서의 구성.jpg" alt="그림 1-2 프로세서의 구성" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-2 프로세서의 구성</figcaption>
</figure>


* 레지스터는 용도에 따라 전용 레지스터와 범용 레지스터로 구분할 수 있음
  * 사용자가 정보를 변경할 수 있다면 사용자 가시(user-visible) 레지스터
    * 사용자 가시 레지스터는 사용자가 운영체제와 사용자 프로그램을 이용하여 정보를 변경할 수 있는 레지스터
  * 사용자가 정보를 변경할 수 없다면 사용자 불가시(user-invisible) 레지스터
* 저장하는 정보의 종류에 따라 데이터 레지스터,주소 레지스터, 상태 레지스터 등으로 세분화할 수 있음



표 1-1 사용자 가시 레지스터

|                  종류                   |                             설명                             |
| :-------------------------------------: | :----------------------------------------------------------: |
|  데이터 레지스터<br/>DR, Data Register  | 함수 연산에 필요한 데이터를 저장한다. 값, 문자 등을 저장하므로 산술연산이나 논리 연산에 사용하며, 연산 결과로 플래그 값을 저장한다. |
| 주소 레지스터<br />AR, Address Register | 주소나 유효 주소를 계산하는 데 필요한 주소의 일부분을 저장한다. 주소 레지스터에 저장한 값(값 데이터)을 사용하여 산술 연산을 할 수 있다. |

- 주소 레지스터 종류
  - 기준 주소 레지스터: 프로그램을 실행할 때 사용하는 기준 주소 값을 저장한다. 페이지나 세그먼트처럼 블록화된 정보에 접근하는 데 사용한다.
  - 인덱스 레지스터: 유효 주소를 계산하는 데 사용하는 주소 정보를 저장한다.
  - 스택 포인터 레지스터: 메모리에 프로세서 스택을 구현하는 데 사용한다. 스택이나 큐 포인터를 사용한다.



- 사용자 불가시 레지스터는 사용자가 정보를 변경할 수 없는 레지스터

|                         종류                          |                             설명                             |
| :---------------------------------------------------: | :----------------------------------------------------------: |
|        프로그램 카운터<br/>PC, Program Counter        |     다음에 실행할 명령어의 주소를 보관하는 레지스터이다.     |
|     명령어 레지스터<br/>IR, Instruction Register      |        현재 실행하는 명령어를 보관하는 레지스터이다.         |
|              누산기<br/>ACC, ACCumulator              |          데이터를 일시적으로 저장하는 레지스터이다.          |
| 메모리 주소 레지스터<br/>MAR, Memory Address Register | 프로세서가 참조하려는 데이터의 주소를 명시하여 메모리에 접근하는 버퍼 레지스터이다. |
| 메모리 버퍼 레지스터<br/>MBR, Memory Buffer Register  | 프로세서가 메모리에서 읽거나 메모리에 저장할 데이터 자체를 보관하는 버퍼 레지스터이다. |



<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-3 프로세서의 기본 레지스터.jpg" alt="그림 1-3 프로세서의 기본 레지스터" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-3 프로세서의 기본 레지스터</figcaption>
</figure>



## 2. 메모리

* 메모리는 컴퓨터 성능과 밀접
* 메모리 계층 구조를 구성하여 비용, 속도, 용량, 접근시간 등을 상호 보완함
* 메모리 계층 구조는 1950~1960년대 너무 비싼 메인 메모리의 가격 문제 때문에 제안한 방법
* 이 방법은 비용, 속도, 크기(용량)가 다른 메모리를 효과적으로 사용함으로써 시스템의 성능을 향상시킴
* 불필요한 프로그램과 데이터는 보조기억장치에 저장했다가 실행 및 참조할 때만 메인 메모리로 옮기는 원리를 적용한 방법

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-4 메모리 계층 구조.jpg" alt="그림 1-4 메모리 계층 구조" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-4 메모리 계층 구조</figcaption>
</figure>



## 2.1. 레지스터

* 프로세서 내부에 있으며, 프로세서가 사용할 데이터를 보관하는 가장 빠른 메모리



## 2.2. 메인 메모리

* 프로세서 외부에 있으며, 프로세서에서 즉각적으로 수행할 프로그램과 데이터를 저장
* 프로세서에서 처리한 결과를 저장
* 주기억장치 또는 기억장치라고도 함

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-5 메인 메모리의 역할 1.jpg" alt="그림 1-5 메인 메모리의 역할 1" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-5 메인 메모리의 역할 1</figcaption>
</figure>

* 메인 메모리는 다수의 셀(cell)로 구성되며, 각 셀은 비트(bit)로 구성
* 셀이 K비트이면 셀에 2^k 값을 저장할 수 있음
* 메인 메모리에 데이터를 저장할 때는 셀 한 개나 여러 개에 나눠서 저장
* 셀은 주소로 참조하는데, n비트라면 주소 범위는 0 ~ (2^n)-1

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-6 메인 메모리의 주소 지정.jpg" alt="그림 1-6 메인 메모리의 주소 지정" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-6 메인 메모리의 주소 지정</figcaption>
</figure>

* 컴퓨터에 주어진 주소를 물리적 주소라고 하며, 프로그래머는 물리적 주소 대신 수식이나 변수를 사용
* 컴파일러가 프로그램을 기계 명령어로 변환할 때 변수와 명령어에 주소를 할당하는데, 이 주소를 논리적 주소(가상 주소, 프로그램 주소)라고 함
* 컴파일로 논리적 주소를 물리적 주소로 변환, 이 과정을 매핑(mapping: 사상) 또는 메모리 맵(memory map)이라고 함

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-7 메모리 매핑.jpg" alt="그림 1-7 메모리 매핑" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-7 메모리 매핑</figcaption>
</figure>

* 메모리 속도는 메모리 접근시간과 메모리 사이클 시간으로 표현할 수 있음
* 메모리 접근시간은 명령이 발생한 후 목표 주소를 검색하여 데이터 쓰기(읽기)를 시작할 때까지 걸린 시간
* 메모리 사이클 시간은 두 번의 연속적인 메모리 동작 사이에 필요한 최소 지연시간

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-8 메모리 접근시간과 메모리 사이클 시간.jpg" alt="그림 1-8 메모리 접근시간과 메모리 사이클 시간" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-8 메모리 접근시간과 메모리 사이클 시간</figcaption>
</figure>

* 메인 메모리는 프로세서와 보조기억장치 사이에 있음
* 여기서 발생하는 디스크 입출력 방목 현상을 해결하는 역할도 함



## 2.3. 캐시

* 프로세서와 메인 메모리 간에 속도 차이가 나면서 메인 메모리의 부담을 줄이기 위해 캐시를 구현하기도 함

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-9 메인 메모리의 역할 2 - 캐시 추가.jpg" alt="그림 1-9 메인 메모리의 역할 2 - 캐시 추가" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-9 메인 메모리의 역할 2 - 캐시 추가</figcaption>
</figure>

* 처리 속도가 빠른 프로세서와 상대적으로 느린 메인 메모리의 속도 차이를 보완하는 고속 버퍼
* 메인 메모리에서 데이터를 블록단위로 가져와 프로세서에 워드 단위로 전달하여 속도를 높임
  * 블록 단위: 블록 한 단위로 취급할 수 있는 문자, 단어, 레코드가 메모리에는 다수의 셀로 되어 있다고 하니 데이터베이스에서의 레코드 집합의 개념처럼 생각하면 될듯함
  * 위드 단위: 하나의 명령어로 실행될 수 있는 데이터 처리 단위, 예를 들어 32bit CPU라면 워드는 32비트가 됨

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-10 캐시의 역할.jpg" alt="그림 1-10 캐시의 역할" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-10 캐시의 역할</figcaption>
</figure>

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-11 캐시의 기본 동작.jpg" alt="그림 1-11 캐시의 기본 동작" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-11 캐시의 기본 동작</figcaption>
</figure>

* 프로세서는 메인 메모리에 접근하기 전에 캐시에 해당 주소의 자료가 있는지 먼저 확인
* 캐시의 성능은 작은 용량의 캐시에 프로세서가 이후 참조할 정보가 얼마나 들어 있느냐로 좌우
* 프로세서가 참조하려는 정보가 있을 때를 캐시 적중(cashe hit: 캐시 히트)이라 함
* 반대로 프로세서가 참조하려는 정보가 없다면 캐시 실패(cashe miss: 캐시 미스)이라 함
* 두 지역성 특성 때문에 블록의 크기는 캐시의 성능으로 좌우됨
  * 공간적 지역성: 대부분의 프로그램이 참조한 주소와 인접한 주소의 내용을 다시 참조하는 특성
  * 시간적 지역성: 한 번 참조한 주소를 곧 다시 참조하는 특성
* 해당 특성이 발생하는 이유
  * 프로그램이 명령어를 순차적으로 실행하는 경량이 있어 명령어가 특정 지역 메모리에 인접해 있음
  * 순환(단일 순환, 중첩 순환 등) 때문에 프로그램을 반복하더라도 메모리는 일부 영역만 참조함
  * 대부분의 컴파일러를 메모리에 인접한 블록에 배열로 저장. 따라서 프로그램이 배열 원소에 순차적으로 자주 접근하므로 지역적인 배열 접근 경향이 있음
* 해당 특성의 크기에 대한 장점과 단점
  * 장점: 블록이 크면 캐시의 히트율이 올라갈 수 있음
  * 단점: 블록이 커지면 이에 따른 전송 부담과 캐시 데이터 교체 작업이 자주 일어나므로 블록 크기를 무작정 늘릴 수 없음



## 2.4. 보조기억장치

* 주변장치 중 프로그램과 데이터를 저장하는 하드웨어로, 2차 기억장치 또는 외부기억장치라고도 함
* 자기디스크, 광디스크, 자기테이프 등이 있음



## 3. 시스템 버스

* 시스템 버스는 하드웨어를 물리적으로 연결하여 서로 데이터를 주고받을 수 있게 하는 통로

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-12 시스템 버스.jpg" alt="그림 1-12 시스템 버스" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-12 시스템 버스</figcaption>
</figure>

|    종류     |                             설명                             |
| :---------: | :----------------------------------------------------------: |
| 데이터 버스 | 프로세서와 메인 메모리, 주변장치 사이에서 데이터를 전송한다. |
|  주소 버스  | 프로세서가 시스템의 구성 요소를 식별하는 주소 정보를 전송한다. |
|  제어 버스  |    프로세서가 시스템의 구성 요소를 제어하는 데 사용한다.     |



## 4. 주변장치

* 주변장치는 프로세서와 메인 메모리를 제외한 나머지 하드웨어 구성요소를 말함
* 입력장치: 컴퓨터에서 처리할 데이터를 외부에서 입력하는 장치
* 출력장치: 입력장치와 반대로 컴퓨터에서 처리한 데이터를 외부로 보내는 장치
* 저장장치: 메인 메모리와 달리 거의 영구적으로 데이터를 저장하는 장치, 저장한 데이터를 출력하는 공간이므로 입출력장치에 포함하기도 함



# 02 컴퓨터 시스템의 동작

* 작업 처리 동작은 제어장치가 동작을 제어
  * ❶ 입력장치로 정보를 입력받아 메모리에 저장한다.
  * ❷ 메모리에 저장한 정보를 프로그램 제어에 따라 인출하여 연산장치에서 처리한다.
  * ➌ 처리한 정보를 출력장치에 표시하거나 보조기억장치에 저장한다.
* 입력장치로 컴퓨터에 유입되는 정보는 명령어와 데이터
  * 여기서 명령어는 실행할 산술 및 논리 연산의 동작을 명시하는 문장, 어떤 작업을 수행하는 명령어 집합의 프로그램으로 컴파일러 등을 이용하여 0과 1로 이진화된 기계 명령어로 변환해야 컴퓨터가 이해가능



## 1. 명령어의 구조

* 명령어는 프로세서가 실행할 연산인 연산 부호와 명령어가 처리할 데이터, 데이터를 저장한 레지스터나 메모리 주소인 피연산자로 구성

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-13 명령어의 기본 구조.jpg" alt="그림 1-13 명령어의 기본 구조" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-13 명령어의 기본 구조</figcaption>
</figure>

* 연산부호 (OPcode OPeration code: 오피코드): 프로세서가 실행할 동작인 연산을 지정, 산술 연산(+, -, *, /), 논리 연산(AND, OR, NOT), shift, 보수 등 연산을 정의
* 연산 부호가 n비트이면 최대 2^n개 연산이 가능
* 피연산자 (operand: 오퍼랜드): 연산할 데이터 정보를 저장, 보통 데이터 자체보다는 데이터의 위치를 저장

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-14 소스 피연산자와 목적지 피연산자.jpg" alt="그림 1-14 소스 피연산자와 목적지 피연산자" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-14 소스 피연산자와 목적지 피연산자</figcaption>
</figure>

* 명령어는 실행 전에 메인 메모리에 저장하며, 한 번에 하나씩 프로세서에 순차적으로 전송하여 해석 및 실행
* 피연산자 수에 따라 0-주소 명령어, 1-주소 명령어 ..... n-주소 명령어 등으로 구분

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-15 메인 메모리에 저장된 명령어 예.jpg" alt="그림 1-15 메인 메모리에 저장된 명령어 예" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-15 메인 메모리에 저장된 명령어 예</figcaption>
</figure>

* 명령어에 피연산자의 위치를 명시하는 방법(직접 주소 및 간접 주소)을 나타내는 모드 비트(mode bit) I를 추가하거나, 다음 명령어의 위치를 나타내는 주소를 추가할 수도 있음
  * 직접 주소: 접근이 한번에 이뤄지는 유효한 주소, 필드 길이가 가변형
  * 간접 주소: 직접 주소를 가르키는 주소, 한번에 처리 가능한 길이로 결정, 하지만 두번 접근 필요

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-16 모드 비트를 추가한 명령어 형식.jpg" alt="그림 1-16 모드 비트를 추가한 명령어 형식" style="border:1px; border-style: solid; zoom:100%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-16 모드 비트를 추가한 명령어 형식</figcaption>
</figure>

* 예를 들어  모드가 1비트, 연산 부호가 3비트, 피연산자가 6비트인 명령어에서 모드가 0이면 직접 주소, 0이면 간접 주소

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-17 직접 주소와 간접 주소를 사용한 명령어 예.jpg" alt="그림 1-17 직접 주소와 간접 주소를 사용한 명령어 예" style="border:1px; border-style: solid; zoom:10%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-17 직접 주소와 간접 주소를 사용한 명령어 예</figcaption>
</figure>



## 2. 명령어의 실행

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-18 명령어 실행 과정.jpg" alt="그림 1-18 명령어 실행 과정" style="border:1px; border-style: solid; zoom:20%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-18 명령어 실행 과정</figcaption>
</figure>

* 프로세서의 제어장치가 명령어를 실행
* 프로세서는 메모리에서 명령어를 한 번에 하나씩 인출하고 해석하여 연산
* 명령어를 인출하여 연산 완료한 시점까지를 인출-해석-실행 사이클 또는 인출-실행 사이클이라고 함

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-19 명령어 실행 사이클.jpg" alt="그림 1-19 명령어 실행 사이클" style="border:1px; border-style: solid; zoom:20%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-19 명령어 실행 사이클</figcaption>
</figure>

* 메모리 간접 주소 지정 방법은 세분화된 명령어 사이클과 같이 실행 사이클을 시작하기 앞서 그 데이터의 실제 주소를 기억장치에서 읽어 오는 간접 사이클을 사용하기도 함
* 인터럽트를 처리하려고 인터럽트 사이클을 사용하기도 함
  * 컴퓨터 작동 중에 예기치않은 문제가 발생할 경우에 업무 처리가 계속 될 수 있도록 하는 기능



## 2.1. 인출 사이클

* 명령어 실행 사이클의 첫 번째 단계
* 메모리에서 명령어를 읽어 명령어 레지스터에 저장하고 다음 명령어를 실행하려고 프로그램 카운터를 증가

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-20 인출 사이클 과정.jpg" alt="그림 1-20 인출 사이클 과정" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-20 인출 사이클 과정</figcaption>
</figure>

| 시간 | 레지스터 동작      | 설명                                                         |
| :--: | :----------------- | :----------------------------------------------------------- |
|  1   | PC -> MAR          | PC에 저장된 주소를 프로세서 내부 버스를 이용하여 MAR에 전달한다. |
|  2   | Memory(MAR) -> MBR | MAR에 저장된 주소에 해당하는 메모리 위치에서 명령어를 인출한 후 이 명령어를 MBR에 저장한다. |
|  2   | PC+1 -> PC         | 다음 명령어를 인출하려고 PC를 증가시킨다.                    |
|  3   | MBR -> IR          | MBR에 저장된 내용을 IR에 전달한다.                           |

PC: 프로그램 카운터

MAR: 메모리 주소 레지스터

MBR: 메모리 버퍼 레지스터

IR: 명령어 레지스터



## 2.2. 실행 사이클

* 인출한 명령어를 해독하고 그결과에 따라 제어 신호를 발생시켜 명령어를 실행



## 2.3. 간접 사이클

* 실행 사이클은 명령어를 수행하기 전에 실제 데이터가 저장된 주기억장치의 주소인 유효 주소를 한 번 더 읽어 온다.

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-21 간접 사이클 과정.jpg" alt="그림 1-21 간접 사이클 과정" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-21 간접 사이클 과정</figcaption>
</figure>

| 시간 | 레지스터 동작      | 설명                                                         |
| :--: | ------------------ | ------------------------------------------------------------ |
|  1   | IR(addr) -> MAR    | IR에 저장된 명령어의 피연산자(주소부)를 MAR에 전달한다.      |
|  2   | Memory(MAR) -> MBR | MAR에 저장된 주소에 해당하는 메모리 위치에서 데이터를 인출한 후 이 데이터를 MBR에 저장한다. |
|  3   | MBR -> IR(addr)    | MBR에 저장된 내용을 IR에 전달한다.                           |

IR: 명령어 레지스터

MAR: 메모리 주소 레지스터

MBR: 메모리 버퍼 레지스터



## 2.4. 인터럽트 사이클

* 프로세서가 프로그램을 수행하는 동안 컴퓨터 시스템의 내부나 외부에서 발생하는 예기치 못한 사건을 의미
* 프로세서는 실행 사이클을 완료한 후 인터럽트 요구가 있는지 검사
* 인터럽트 요구가 없다면 다음 명령어 인출
* 인터럽트 요구가 있다면 현재 수행 중인 프로그램의 주소(프로그램 카운터) 값을 스택이나 메모리의 0번지와 같은 특정 장소에 저장
  * 그 뒤, 프로그램 카운터에는 인터럽트 처리 루틴의 시작 주소를 저장해 두었다가 처리를 완료하면 중단된 프로그램으로 복귀

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-22 인터럽트 사이클 과정.jpg" alt="그림 1-22 인터럽트 사이클 과정" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-22 인터럽트 사이클 과정</figcaption>
</figure>

| 시간 | 레지스터 동작            | 설명                                                  |
| :--: | ------------------------ | ----------------------------------------------------- |
|  1   | PC -> MBR                | PC의 내용을 MBR에 저장한다.                           |
|  2   | IntRoutine_Address -> PC | 인터럽트 루틴 주소를 PC에 저장한다.                   |
|  2   | Save_Address -> MAR      | PC에 저장된 인터럽트 루틴 주소를 MAR에 저장한다.      |
|  3   | MBR -> Memory(MAR)       | MBR의 주소에 있는 내용을 지시된 메모리 셀로 이동한다. |

PC: 프로그램 카운터

MAR: 메모리 주소 레지스터

MBR: 메모리 버퍼 레지스터



## 3. 인터럽트 명령어

* 현재 실행 중인 프로그램을 중단하고 다른 프로그램의 실행을 요구하는 명령어
* 프로그램이 실행 순서를 바꿔 가면서 처리하여 다중 프로그래밍에 사용, 시스템의 처리 효율을 향상
* 예상치 못한 사용자 입력, 갑작스런 정전, 컴퓨터 시스템에서 긴급 요청, 잘못된 명령어 수행, 입출력 작업 완료와 같은 상황을 시스템이 적절히 처리하는데 필요
* 사용자가 별도로 인터럽트 조치를 할 필요가 없고 프로세서와 운영체제가 처리
* 컴퓨터는 인터럽트를 외부장치의 동작과 자신의 동작을 조정하는 수단으로 사용
  * ex) 키보드 동시입력, 프린트 ..
* 이를 통해서 오버헤드가 증가하거나 수행 시간이 낭비되는 사태를 예방가능
* 입출력장치가 준비 상태가 될 때까지 프로세서가 다른 작업을 수행할 수 있음
* 제어 버스 중 이런 목적으로 사용하는 것이 바로 인터럽트 요청 회선(IRQ, Interrupt ReQuest line)
  * 해당 회선을 사용하면 입력이 발생했을 때만 프로세서에 통보 및 처리하므로 이벤트 발생 여부를 일일이 감시하지 않아도됨
* 인터럽트는 크게 인터럽트 요청과 인터럽트 서비스 루틴으로 구분
* 인터럽트 요청 회선은 단일 회선과 다중 회선으로 연결할 수 있음
  * 단일 회선: 인터럽트 요청이 가능한 모든 장치를 공통의 단일 회선으로 프로세서에 연결하는 방법, 회선 하나에 장치를 여러 개 연결하여 인터럽트를 요청한 장치를 판별하는 기능이 필요
  * 다중 회선: 모든 장치를 서로 다른 고유의 회선으로 프로세서와 연결하는 방법, 요청한 장치를 바로 판별할 수 있음

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-23 인터럽트 요청 회선 연결 방법.jpg" alt="그림 1-23 인터럽트 요청 회선 연결 방법" style="border:1px; border-style: solid; zoom:40%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-23 인터럽트 요청 회선 연결 방법</figcaption>
</figure>

<figure style="display:block; text-align:center;">
    <img width="500" src="..\img\그림으로 배우는 구조와 원리 운영체제\Chapter1\그림 1-24 인터럽트 처리 과정.jpg" alt="그림 1-24 인터럽트 처리 과정" style="border:1px; border-style: solid; zoom:15%;"/>
    <figcaption style="text-align:center; font-weight:bold; font-size:80%;">그림 1-24 인터럽트 처리 과정</figcaption>
</figure>

* 인터럽트는 문제가 발생했을 때 실행 중인 프로그램과 관련이 없을 수도 있음
* 따라서 인터럽트가 발생할 때의 상태 코드(상태 워드)를 임시 기억장치에 저장해 두었다가 나중에 복귀했을 때 이를 다시 적재해야함
* 이래야 원래 프로그램을 인터럽트의 영향을 받지 않고 다시 실행할 수 있음



