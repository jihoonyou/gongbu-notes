# unity

## 개요/목표
- 사이드 프로젝트를 위한 유니티 공부

## 공부자료
- 튜토리얼
- [] [2D 튜토리얼](https://www.youtube.com/playlist?list=PLctzObGsrjfxSys0Tdq9vPl_YGVYSI337)
- [] [유니티 UNet](https://www.youtube.com/playlist?list=PLctzObGsrjfxQ6A8KX1heuQaNkL5xMA2D)
- [] [유니티 포톤](https://www.youtube.com/playlist?list=PLctzObGsrjfwF7kkoraWb235U8Z602gx1)
- 강의
- [] [retr0의 유니티](https://www.udemy.com/course/retr0-unity/)

## 유니티 준비하기
### 유니티 허브와 유니티 데이터 설치
- Unity hub는 여러버전의 유니티를 한 컴퓨터에서 동시에 관리할 수 있게 해주는 launcher
  - 우리 프로젝트에서는 2021.3.20f1 사용예정

### 새 프로젝트 생성 + 인터페이스 살펴보기
- New Project
- Template은 프로젝트 생성 후, 추후 변경 가능
- interface
  - default -> 2 by 3
  - Scene, Hierarchy, Inspector
  - Game, Project, Console
- Unity는 하나의 게임 world를 scene단위로 단위
- Scene: 작업화면을 보여주는 듯
- Game: 실제 플레이어가 볼 화면 프리뷰 (Main Camera가 보고 있는 화면)
- Hierarchy: 현재 존재하는 것을 리스트업
  - Main Camera: 플레이어가 보게 될 화면
  - Directional Light: 씬에 빛을 만듦
- Inspector: game object의 정보(게임 세상에 존재하는 물건이나 사물), component(해당 게임 object에 동작을 부여할 수 있는 부품)
  - game object에 기능을 추가하고 싶다면, 해당 기능을 갖고 있는 component를 해당 game object에 추가
- Project: 현재 프로젝트에서 사용할 모든 에셋과 패키지 표시
  - 에셋: 프로젝트에서 사용할 모든 파일(이미지, 음악, 비디오, 3D모델, 애니메이션, 스크립트, ...)
  - Packages: 패키지 매니지 모듈을 통해 추가된 외부 모듈
- Console

### 플레이버튼
- play, pause, step(한 프레임씩 진행)
  - play 모드중에 scene에 적용된 사항은 play 모드가 해제되면 모두 사라진다

### 트랜스폼 툴 + 씬 탐색
- 트랜스폼 툴: scene창에서 돌아다니고 게임 Object 편집 (q(option, scroll button) ,w,e,r,t,y)
- pivot, local로 변경

### 기즈모 + 씬 기즈모
- 기즈모: scene 창에 개발에 편의를 위해 표시되는 도구
- 씬 기즈모: scene 카메라의 방향과 시점 파악 및 변경

### 트랜스폼 툴 + 오브잭트 변형
- moveTool
- rotateTool
- scaleTool
- rectTool: 가로 세로 방향의 크기만 편집
- TransformTool: 다 합친 것

### 씬 에셋
- Hierarchy에서 cmd + n -> cmd + s

### 피벗-센터 + 로컬-글로벌 전환
- 피벗: object 기준
- 센터: object의 기준
- 로컬: 선택한 게임 오브젝트의 기준
- 글로벌: 글로벌 좌표계를 기준
- 게임 오브젝트 편집시 (피컷-로컬 추천)

### 프로젝트 폴더 구조 + 프로젝트 다시 열기
- 유니티프로젝트 필수 폴더: Assets, Packages, ProjectSettings

## 게임 엔진의 원리
### 게임 오브젝트와 컴포넌트

- 게임엔진: low-level을 감싸고 있는 이미 완성된 기반 코드 제공
- 상속개념 설명
- 유니티  Game Object - Component (Component Pattern -A has B)
    - 필요한 기능이 있으면 그 object를 포함시키는 것
    - 게임 오브젝트(게임 안의 사물) - 단순 holder, 빈 껍데기
        - 컴포넌트(스스로 동작하는 독립 부품)를 붙일 수 있음
            - 미리 만들어진 부품
            - 각자 대표 기능을 가진다
    - 장점: 유연한 재사용, 독립성 덕분에 추가 삭제가 용이, 기획자의 프로그래머 의존도가 낮아짐
- Cube Game Object 예시
    - Cube Game Object자체는 특별한 기능을 갖고 있지 않음
    - Transform Component: 위치, 크기, 회전을 가질 수 있는 능력 부여
    - Mesh Filter: 그래픽 외곽선
    - Mesh Renderer: 외곽선을 따라 색을 채워줌
    - Box Collider: 물리적인 표면을 만들어 충돌 가능하게 (이거 지우면 물리적인 표면이 존재하지않아, 뚫고 지나가게 됨
    - 중력을 적용하게 싶으면, Physics/RigidBody
- Component를 조립하여 로직에 집중할 수 있음

## 게임 엔진의 원리
### 메시지와 브로드캐스팅

- 각 컴포넌트는 어떻게 외부의 간섭없이 스스로가 동작할 수 있을까?
- 컴포넌트는 MonoBehaviour를 상속 받음
    - 컴포넌트로서 게임 오브젝트에게 추가될 수 있다
    - 유니티의 통제를 받는다
    - 유니티 이벤트 메시지를 감지할 수 있게 된다
- 메시지: 실행해야하는 기능을 담고 있는 정보 (누가 받는지, 누가 보냈는지 신경 x, 메시지에 명시된 기능이 있으면 실행, 없으면 무시
- 브로드캐스팅: 메시지를 무차별적으로 많이 보내는 것
    - Dance() broadcasting,
    - Start()
        - 게임 도중 새로 추가된 게임오브젝트도 자동실행
- 유니티 이벤트 메서드: 이름만 맞춰 구현하면, 해당 타이밍에 자동 실행된다
- 정리: 유니티의 모든 컴포넌트는 MonoBehaviour 기반, 컴포넌트는 메시지를 받을 수 있다, 메시지에 해당하는 기능을 가지고 있으면 실행한다, 이벤트 기반 메서드는 메시지를 통해 실행 되야할 타이밍에 자동 실행된다