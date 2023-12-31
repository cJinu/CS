# MVC Pattern
  - ![image](https://github.com/cJinu/CS/assets/38110757/eabe07fc-a968-4089-9ed9-31cf78d8709e)
  - 정의: Model, View, Controller로 이루어진 디자인 패턴
  - Model: Application의 데이터인 데이터베이스, 상수, 변수 등을 의미
    - 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야만 함
    - view나 controller에 대해 어떠한 정보도 알지 말아야 함
    - 변경이 일어나면 변경 통지에 대한 처리 방법을 구현해야 함
  - View: 사용자의 인터페이스 요소, 모델을 기반으로 사용자가 볼 수 있는 화면
    - 모델이 가지고 있는 정보를 따로 저장해서는 안됨
    - model이나 controller와 같은 다른 구성 요소들을 몰라야 됨
    - 변경이 일어나면 변경 통지에 대한 처리 방법을 구현해야만 함
  - Controller: 하나 이상의 model과 하나 이상의 view를 잇는 다리 역할, 이벤트 등 메인 로직을 담당
    - model이나 view에 대해서 알고 있어야 함
    - model이나 view의 변경을 모니터링 해야 함
  - 역할 분담의 가이드라인(어떻게 나눌 것인가)
  - 서로 분리되어 각자의 역할에 집중적으로 개발 가능(효율적)
  - 유지보수성, 확장성, 유연성 증가
  - 중복 코딩이 일어날 경우가 없음
  - Model 1
    - ![image](https://github.com/cJinu/CS/assets/38110757/94787e30-4680-4b4e-a93a-5b4711bbb863)
    - Controller와 view를 같이 구현하는 방식
    - 사용자의 요청을 전부 jsp가 처리 → 구현이 쉬움
    - 프로젝트의 크기가 커질수록 재사용성이 떨어지고 읽기가 힘들어짐 → 유지보수성 감소
    - 협업하기 힘들다 → 거의 안 씀
  - Model 2
    - ![image](https://github.com/cJinu/CS/assets/38110757/46d218be-feb4-4381-9d48-84f12180265d)
    - Controller(java code)와 view(html source)가 분리된 형태
    - 사용자 요청을 servlet(controller)가 받음
    - 역할의 분리로 인해 유지보수성 극대화
    - 구조가 복잡해짐 → spring framework로 극복
  - Java Bean
    - 특정한 정보를 가지고 있는 class를 표현하는 하나의 규칙
    - 데이터에 규칙을 부여하여 편리하게 사용하기 위함
    - 반드시 class는 패키지화 되어야 함
    - 변수(property)는 private, getter와 setter는 public
    - 위의 규칙을 따르는 class를 java bean이라 부름
    - 쉽게 Dto라고 생각하면 됨, MVC Pattern에서 데이터를 표현해주는 Model에서 사용하기 위한 표현의 형태
  - Spring MVC
    - ![image](https://github.com/cJinu/CS/assets/38110757/9b1cf3d2-13cd-4bb0-ad64-b0ca7b67c0f4)
    - Front controller인 DispatcherServlet은 사용자의 모든 요청을 받고, 그 요청을 분석하여 세부 컨트롤러(Handler)에게 위임
    - 비즈니스 로직 처리 결과는 model에 담겨 다시 front controller에 전달
    - 받은 model을 알맞은 view에 전달 후 결과 화면 return
# MVP Pattern
  - ![image](https://github.com/cJinu/CS/assets/38110757/bb789bf1-1cf8-41ed-a581-0d6316db5bf0)
  - 정의: Mode, View, Presenter로 이루어진 디자인 패턴
  - Presenter: View에서 요청한 정보로 model을 가공하여 view에 전달
  - presenter와 view는 1:1 관계
  - MVC 패턴의 단점이던 model과 view 사이의 높은 의존성을 해결
  - 대신 view와 presenter 사이의 의존성이 높음
- MVC Pattern과 MVP Pattern의 차이
  1. MVC Pattern의 cotroller와 view는 1:n 관계, MVP Pattern의 presenter와 view는 1:1 관계
  2. MVC Pattern은 view와 model의 의존성이 높음, MVP Pattern은 view와 presenter의 의존성이 높음
# MVVM Pattern
  - ![image](https://github.com/cJinu/CS/assets/38110757/496e9823-2fe9-4bff-b47d-15872eef0b30)
  - 정의: Model, View, View Model로 이루어진 디자인 패턴
  - View Model: View를 표현하기 위해 만든 View를 위한 Model
  - 중요: Command Pattern, Data Binding → View와 View Model 사이의 의존성 zero
  - View Model과 View는 1:n 관계
  - Data Binding: View Model의 logic이 바뀌면 View도 동기화 → 데이터의 일관성 유지
  - Command Pattern: View에 action이 들어오면, command 패턴으로 view model에 action을 전달
