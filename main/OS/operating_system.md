# 운영체제와 컴퓨터

## 운영체제의 역할과 구조

- 하드웨어와 소프트웨어(유저 프로그램)를 관리
- 유저가 컴퓨터를 편하게 사용할 수 있도록 하드웨어 자원을 관리
- 사용자가 직접적으로 하드웨어에 접근하는 것을 방지

### 운영체제의 역할

1. CPU 스케줄링과 프로세스 관리: CPU 소유권을 어떤 프로세스에 할당할지, 프로세스의 생성과 삭제, 자원 할당 및 반환을 관리
2. 메모리 관리: 한정된 메모리를 어떤 프로세스에 얼만큼 할당해야 하는지 관리
3. 디스크 파일 관리: 디스크 파일을 어떠한 방법으로 보관할지 관리
4. I/O 디바이스 관리: I/O 디바이스들과 컴퓨터 간에 데이터를 주고받는 것을 관리

### 운영체제의 구조

![image](https://github.com/cJinu/CS/assets/38110757/ba9f1ba5-2964-4fad-ab0c-1ae70af75b7b)

- 인터페이스: 사용자의 명령을 컴퓨터에 전달하고 결과를 사용자에게 알려주는 소통의 역할
- GUI: 사용자가 전자장치와 상호 작용할 수 있도록 하는 사용자 인터페이스의 한 형태, 단순 명령어 창이 아닌 아이콘을 마우스로 클릭하는 단순한 동작으로 컴퓨터와 상호 작용할 수 있게 해준다.
- CUI: 그래픽이 아닌 명령어로 처리하는 인터페이스
- 커널: 전반적인 프로세스, 메모리, 하드웨어 관리 등 컴퓨터에 속한 자원을 관리하는 역할, 추상화 계층

![image](https://github.com/cJinu/CS/assets/38110757/b2c77f3f-0e49-4c26-9f6c-1541250357f4)

- 드라이버: 하드웨어를 제어하기 위한 소프트웨어(ex. 프린터 드라이버 설치)
- 시스템콜: 운영체제가 커널에 접근하기 위한 인터페이스, 유저 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출할 때 사용
  - 사용자나 프로그램이 직접적으로 컴퓨터 자원에 접근하는 것을 방지 → 커널 보호

## 시스템콜

- 운영체제가 하드웨어를 다루기 위해 입출력, 메모리 할당, 프로세스 생성 등을 수행하는 코드의 집합
- 컴퓨터 구조(CPU 구조)와 OS에 따라서 다양하게 구현
- 운영체제가 컴퓨터를 제어하는 2가지 방식 존재(유저 모드, 커널 모드)
- 컴퓨터가 CPU를 어떻게 사용하느냐에 따라 달라짐
- 유저 모드: 사용자와 데이터를 왔다갔다할 수 있는 등의 작업, CPU의 명령어를 마음대로 설정할 수 없음
- 커널 모드: 운영체제 내부에서 실제로 하드웨어를 제어, CPU를 직접 제어
- 시스템콜을 통한 요청에 따라 모드를 변경

![image](https://github.com/cJinu/CS/assets/38110757/f5077bb2-a0bb-4af0-b865-37ad8e4e818f)

- 유저 모드에서 어플리케이션 작업 요청을 보냄 → 커널모드에서 CPU한테 작업을 수행하라고 명령
- CPU가 메인 메모리에서 특정 코드와 데이터를 가져와 작업
- 키보드 입력은 우선순위가 매우 높은 작업 → 키보드 인터럽트라는 시스템콜을 호출하여 하던 일을 멈추고 키보드에 대한 처리

### 멀티 프로세싱

- 멀티코어 환경에서는 각 코어가 각 시스템콜을 각자 처리 가능(병렬적 처리)
- 여러 작업들이 동시에 이루어지게 보이는 핵심적인 이유는 굉장히 빠르게 처리되기 때문

### 시스템콜의 유형

1. Process Control: 어떤 작업을 시작하고 어떤 작업을 멈출지 정해주는 시스템콜
2. File Management: 파일 다운로드, 저장, 삭제 등의 작업(문서 작업)
3. Device Management: IO 디바이스를 운영체제에서 시스템콜 형태로 관리
4. Information Maintenance: 현재 컴퓨터에서 작동하고 있는 모든 정보, 상태들을 관리(ex. 시간)
5. Communications(computer ↔ computer): 컴퓨터와 다른 컴퓨터 사이의 소통(네트워크) 관리(ex. 블루투스, 와이파이, 에어드랍)

### Modebit

- IO 디바이스는 운영체제를 통해서만 작동해야 함
- 시스템 자원 보호

![image](https://github.com/cJinu/CS/assets/38110757/191f1682-a29e-48cf-bbd9-a3dd6dbafe62)

## 컴퓨터의 요소

### CPU

- 산술논리연산장치, 제어장치, 레지스터로 구성되어 있는 컴퓨터 장치
- 인터럽트에 의해 단순히 메모리에 존재하는 명령어를 해석해서 수행
- 커널(관리자 역할)이 프로그램을 메모리에 올려 프로세스로 만들면 CPU가 이를 처리
- 폰노이만 구조

![image](https://github.com/cJinu/CS/assets/38110757/a20f1087-c9b0-4f63-9c10-98d96586d9fe)

- 제어장치: 프로세스 조작을 지시하는 CPU의 한 부품
  - 입출력장치 간 통신을 제어
  - 명령어들을 읽고 해석
  - 데이터 처리를 위한 순서를 결정
- 레지스터: CPU 안에 있는 매우 빠른 임시기억장치
  - CPU와 직접 연결 → 연산 속도가 메모리보다 수십 배에서 수백 배까지 빠름
  - CPU는 레지스터를 거쳐 데이터를 전달
  - 캐시메모리(L3, L2, L1)
  - 범용 레지스터: 연산에 필요한 데이터나 연산 결과를 임시로 저장
  - 특수목적 레지스터
    - 메모리 주소 레지스터: 읽기와 쓰기 연산을 수행할 주기억장치 주소 저장
    - 프로그램 카운터: 다음에 수행할 명령어 주소 저장
    - 명령어 레지스터: 현재 실행 중인 명령어 저장
    - 메모리 버퍼 레지스터: RAM에서 읽어온 데이터나 저장할 데이터 임시 저장
    - AC(누산기): 연산 결과 임시 저장
- 산술논리연산장치: 두 숫자의 산술 연산과 논리 연산을 계산하는 디지털 회로
- 버스: CPU와 다른 시스템 구성요소들(메모리, 입출력 장치 등) 간에 데이터나 메모리를 전송하는 경로

### CPU의 연산 처리

![image](https://github.com/cJinu/CS/assets/38110757/62a9fc91-455b-4d2c-92f8-7566ab75128e)

1. 제어장치가 메모리와 레지스터에 계산할 값을 로드
2. 제어장치가 레지스터에 있는 값을 계산하라고 산술논리연산장치에 명령
3. 제어장치가 계산된 값을 다시 레지스터에서 메모리로 계산한 값을 저장

### CPU의 명령어 처리

1. 인출: RAM에서 명령어를 인출하여 버스를 통해 레지스터로 옮기는 단계
2. 해석: 레지스터가 데이터를 제어장치에 전달하고 명령어를 해석하는 단계
3. 실행: 해석된 명령어를 ALU에 전달해주고 연산을 하는 단계
4. 저장: 연산된 값을 다시 레지스터에 저장하는 단계

### 명령어 세트

- CPU가 실행할 명령어 집합
- 연산코드 + 피연산자
- 연산 코드: 연산, 제어, 데이터 전달, 입출력 기능 등 실행할 연산
- 피연산자: 주소, 숫자/문자, 논리 데이터 등 필요한 데이터 저장

![image](https://github.com/cJinu/CS/assets/38110757/559f0bbc-eae7-4f42-87ed-00e02ff2eb80)

### 인터럽트

- 어떤 신호가 들어왔을 때 CPU를 잠깐 정지시키는 것
- 명령어 실행을 마칠 때마다 중앙처리장치는 반복적으로 인터럽트 요청이 있는지 확인
- IO 디바이스로 인한 인터럽트, 산술 연산(0으로 나누는 연산)에서의 인터럽트, 프로세스 오류
- 하드웨어 인터럽트: IO 디바이스에서 발생하는 인터럽트
  - 타이머 인터럽트, 입출력 인터럽트(입출력 장치는 속도가 상대적으로 느림)
- 소프트웨어 인터럽트(trap): 프로세스 오류 등으로 프로세스가 시스템콜을 호출할 때 발생
  - 실행할 수 없는 명령어, 명령어 실행 오류

![image](https://github.com/cJinu/CS/assets/38110757/30021d00-c9e4-44b1-8051-3fc180477f74)

### 인터럽트 핸들러

- 인터럽트를 처리하기 위한 루틴
- 인터럽트 요청에 대응하기 위한 특정 기능을 수행하는 함수

### DMA 컨트롤러

- IO 디바이스가 메모리에 직접 접근할 수 있도록 하는 하드웨어 장치
- CPU는 너무 많은 인터럽트 요청을 받음 → 보조적으로 CPU의 일을 부담하며 CPU 부하를 막아줌
- 하나의 작업을 CPU와 DMA 컨트롤러가 동시에 하는 것을 방지

![image](https://github.com/cJinu/CS/assets/38110757/b2d7991b-b70b-4d0e-9a49-50eaf19f2c3d)

### 메모리

- 전자회로에서 데이터나 상태, 명령어 등을 기록하는 장치
- 메모리가 크면 클수록 많은 일들을 동시에 수행 가능
- 주기억창치(RAM): 휘발성 메모리, 용량이 상대적으로 작음
- 보조기억장치(HDD/SSD): 비휘발성, 용량이 큼

### 타이머

- 특정 프로그램(시간이 많이 걸리는 프로그램)이 작동할 때 제한을 검

### 디바이스 컨트롤러

- IO 디바이스들의 작은 CPU
- 각 디바이스에서 데이터를 임시로 저장하게 하기 위해 로컬 버퍼가 옆에 붙어있음
