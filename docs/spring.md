# spring

## 개요/목표
- 강의를 들으며 interview questions의 답을 찾아간다.
- 전체적인 흐름을 이해하고, 어떤 것인지 알고, 인터뷰 질문에 대답할 수 있는 수준을 목표로 한다.
- 기본 강의 1회독을 통한, 이해 또는 스프링 프레임워크에 대한 익숙함을 더하는 것을 목표로 한다. 

## 공부자료
- [ ] [spring 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/dashboard)
- [ ] [네이버 부스트코스 스프링프로젝트](https://www.boostcourse.org/web316/joinLectures/12943) 추후진행 필요
### 스프링 개요

#### Spring Framework
- 주요기능: DI, AOP, MVC, JDBC를 제공
    - 프로그램 방법론임
- 차의 네비게이션같은 기능

#### 스프링 프레임워크 모듈
- core, aop, jdbc, tx, webmvc와 같은 모듈이 있다.
    - 라이브러리로 제공
    - 필요한 모듈을 골라 사용

#### 스프링 컨테이너(IoC)
- 객체를 생성하고 조립하는 container로 
    - 컨테이너를 통해 생성된 객체를 Bean이라고 함
    - 자바에서는 객체 = 스프링에서는 Bean인듯?
    - spring container = 그릇

### 스프링 프로젝트 생성

#### Maven
- maven: build tool
    - create-react-app같은 건가?
- group id: 내 프로젝트를 감싸고 있는 이름
    - 지하철 호선 전체
- artifact id: 현재 프로젝트 이름
    - 각 호선 프로젝트
- porm.xml
    - 모듈등 필요한 기능을 가져오기 위함
    - package.json 같은 건가?
    - dependency에 필ㄹ요한 라이브러리 명시
        - 그러면, maven dependencies에 라이브러리가 들어가는듯
    - build될 때 명령어
- 프로젝트 생성 구조
    - 프로젝트 폴더 안
        - src/main/java
            - java 언어를 이용해 기능 구현해 나가는 곳
        - src/main/resources
            - 빌드 및 개발 환경 파일이 모여있음
            - 스프링 설정파일(XML) 또는 프로퍼티 파일 등이 관리
        - porm.xml: 메이븐 설정파일로 메이븐은 라이브러리를 연결해주고, 빌드를 ㅇ위한 플랫폼
            - 필요한 라이브러리만 다운로드!
            - Maven depedencies에 다운


#### Spring 자바 프로젝트와의 차이
- porm.xml을 통해 spring의 다양한 모듈들을 이용해 개발하는 것
    - 요즘은 annotation많이 쓰는듯?
- applicationContext.xml
    - spring continaer에 bean을 만들어주는 곳
    - bean으로 명시하면 자동으로 객체가 생성되서 memory에 load됨, 굳이 new로 생성 안해도 된다
    - 스프링 컨테이너에 담겨있다
- xml파일로 객체를 생성하는 것을 고안
    - spring container
        - bean
    - getBean

#### 이클립스 없이 프로젝트 생성
- 직접 폴더 생성하고, porm.xml생성하면 됨

### 의존객체
#### Dependency Injection
- 방법론 중 하나임 (스프링외에 다른곳에서도 사용)
- DI란
    - 배터리 일체형
        - 배터리가 떨어지면 장난감을 새로 구입해야함
        - 생성자에서 배터리 주입
    - 배터리 분리형
        - 배터리가 떨어지면 배터리만 교체하면 된다
        - setBattery 함수로 교체
        - 생성자에서 주입하고, 다 떨어지면, setBattery 함수로 주입
    - 객체 지향 입장으로 모든게 연결되어있으면.. 일체형은 교체 불가능
    - 객체를 분리가능하게 만들어 쓸모있는 것을 넣고 빼는 것
    - 유연성있게!
- DI: 객체를 만들어서 외부에서 따로 주입하는 것
    - 객체에 의존하여 주입
- 스프링에서의 의존 주입
    - 스프링 컨테이너안에서 의존 주입
    - 기존 예제에서는 interface Battery를 통해 유연성있게 만듦.
        - ChargeBattery, NormalBattery implements Battery
    - applicationContext.xml에서
        - <Bean><constructor-arg> </Bean>
#### 다양한 의존 객체 주입
- 생성자를 이용한 의존 객체 주입
    - bean으로 객체 생성
    - constructor-arg값응로 넣어주면 됨
- setter를 이용한
    - <property name="set제외하고 소문자값", value= '들어갈 값'>
- List를 이용한
    - <property><llist><value></value>...</list></property>
- Map을 이용한
    - <property><map><key></key><value></value><ref></map></property>

#### 스프링 설정 파일 분리
- 스프링 설정 파일이 길어지기 때문에.. xml 파일 분리 필요!
- applicationCoontext.xml
    - appCtx1.xml
    - appCtx2.xml
    - appCtx3.xml
- 배열 형태로 모아서 입력가능
    - 주로 일반적으로 배열로 사용
- import tag로 사용 가능
    - 이렇게 할 수 있다 정도

#### Bean의 범위
- 싱글톤: getBean을 호출할 때 하나의 객체를 만들어서 공유
    - 객체가 이미 생성되어있음
    - getBean("A"), getBean("B")
        - 동일한 객체를 reference
        - 뭐 주소값이 같은듯.
    - default
- 프로토타입: 싱글톤의 반대
    - scope="prototype"
    - 호출할 때마다 다른 객체 생성

#### 의존객체 자동 주입
- 의존객체 자동 주입
    - 스프링 컨테이너가 필요한 의존 대상 객체를 찾아서 의존 대상 객체가 필요한 객체에 주입해주는 기능
    - @Autowired
    - @Resource
- @Autowired: 주입하려고 하는 객체의 **타입**이 일치하는 객체를 자동으로 주입한다.
    - 객체의 타입을 보고, 타입이 일치하는 것을 찾아서 넣어주는 것
    - constructor-arg을 사용하지 않고, 생성자 위에 @Autowired를 적으면 됨
        - <context:aonntation-config >추가 필요
        - + namespace 추가 필요
        - property 및 method에 넣어서 사용 가능 
            - 주의: 위의 경우는 default constructor를 생성해야함
- @Resource: 주입하려고 하는 객체의 **이름**이 일치하는 객체를 자동으로 주입한다.
    - 객체 타입을 보는 것이 아닌 똑같은 이름을 찾아서 주입
    - 생성자에는 사용 불가

#### 의존객체 선택
- 의존객체 선택
    - 동일한 객체가 2개 이상인 경우 스프링 컨테이너는 자동 주입 대상 객체를 판단하지 못해서 Exception을 발생시킨다.
    - <qualifier value="usedDao">
    - @Qualifier('usedDao')
- @Inject
    - required속성 지원 x (required는 Autowired에서 지원하는데 잘 안씀)
    - @Named(value='객체이름')

- 자주 쓰이는 순서
    - @Autowired > @Required > @Inject

### 생명주기(Life Cycle)
#### 스프링 컨테이너 생명주기
1. GenericXmlApplicationContext() ctx - 스프링 컨테이너 생성
2. getBean() - 빈 객체 이용
3. ctx.close() - 자원해체
- spring container bean 객체의 생성시점은 동일
- getBean으로 불러오는 것
- close()에서 소멸 

#### 빈 객체 생명주기 - interface를 이용하는 방법
- 스프링 컨테이너 초기화 - 빈 객체 생성 및 주입
- 스프링 컨테이너 종료 - bean 객체 소별
- afterProppertySet() -> InitializingBean (interface)
    - bean 생성시점에 특별한 일을 하고 싶을 때
    - ex) db 계정 연결 및 인증
- destroy() -> DispoableBean (interface)
    - 소멸되는 시점에 뭔가를 하고 싶을 때
- 방법: 각 interface들을 implements하고 함수 생성하여 작업 등록!

#### 빈 객체 생명주기 - init-method destory-method
- <bean init-method="메소드이름" destory-method="메소드이름">
    - 각 method이름으로 생성한 함수에 작업 등록!

### annotation을 통한 스프링 설정
#### 자바로 바꾸기
- XML이 아닌 java파일로 스프링 설정 파일을 만듦
- @Configuration : xml처럼 사용
- MemberConfig.java
    - @Bean
    - id가 method 이름으로, Class도 정의
        - return 생성자(arg)
- 타입에 맞춰서 클래스 메소드 또는 생성자를 생성한다고 생각하면 될듯
     
#### 자바 annotation 분리
- 자바파일 쪼개는 것
- @Autowired를 통해 자동 주입
    - 나눈 config java파일들은 다 하나의 container안에 있기 떄문에 자동주입 가능
- AnnotationConfigApplicationContext(class1, class2, class3)

- import annotation
    - 하나의 파일에 나머지 파일들을 import하는 것
    - @Import({Memeberconfig2.class, Memberconfig3.class})
- 본인 스타일에 따라 쓰는 방법이 다름!

### 웹 프로그래밍 설계 모델
- model1
    - client - was(JSP, service & DAO) - database
    - HTML, java, 태그
    - 장점: 개발이 빠름(여러가지 언어를 하나의 문서에 작성)
    - 단점: 유지 보수 및 소스가 헷갈릴 수 있음
- model2
    - client -> contoroller -> service -> dao -> model
    -        <-  view          (기능별 서비스)
    - 기능은 서비스에서, 데이터베이스는 DAO
    - 사용자는 View (JSP)
    - M은 데이터베이스 관련
    - C는 controller
    - 각각의 기능이 분리되어 있어 기능 추가가 쉬움
- MVC 설계 구조
    - client -> DispatcherServlet
        - 1. Handlermapping은 많은 컨트롤러 중에 적합한거 매핑해줌 (가장 적합한 컨트롤러를 찾아줌)
        - 2. HandlerAdapter를 통해, (controller에 적합한 method를 찾아달라함)ㅇㅇㅇㅇ
            - model이라는 data를 가져옴
        - 3. ViewResolver (View에 가장 적합한 JSP 표시)
        - 4. View 응답 생성 (JSP 클라이언트에 전송)
    - 흠.. 이건 그냥 외워야하고, 자주쓰다보면 외워질듯

- DispatcherServlet: 뭔가 사거리, 신호등 같은?
    - 모든 클라이언트의 요청을 이게 처음 받는다?
    - servlet부분을 좀 알아야 할듯?
- @Controller
    - Model & View로 데이터 관리?
- @RequestMapping('/요청')
    - 요청 메핑
- "개발자는 Model 객체에 데이터를 담아서 DispatcherServlet에 전달할 수 있다"
- "DispatcherServlet에 전달된 Model데이터는 View에서 가공되어 클라이언트한테 응답처리된다"
- View객체
    - jsp전달하는듯?
- 정리
    1. client가 요청 -> DispatcherServlet이 받는다(스프링프레임워크에서 web.xml에서 서블릿 등록을하고 그 초기파라미터로 스프링 설정파일을 설정한다)
    2. DispatcherServlet은 Controller를 찾는다 (Handlermapping이 찾아줌 ) (@controller 어노테이션으로 컨트롤러를 만듦)
    3. 적합한 컨트롤러를 찾으면 다시 DispatcherServlet으로 감
    4. 적합한 Method를 찾기 시작한다 (HandlerAdapter가 찾아주는듯?) (@RequestMapping('success')로 success가 사용자가 요청한 값)
    5. 메서드를 찾아서 실행되고나서 service, Dao, Db하고 처리된 후, Model View의 데이터가 옴
    6. ViewResolver를 이용해서 가장 적합한 View를 찾음
    7. 가장 적합한 View를 JSP로 응답 
