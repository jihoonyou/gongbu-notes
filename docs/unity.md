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

## 게임 제작: 소코반(창고지기)
### 초기 씬 구성

- window layout 2 by 3 (기본 세팅)
- Material (shader + texture) -> 물체 색
- Plane과 Player에는 Collider가 있어서 뚫리지 않고 부딫힘
- default가 private
- 코드상의 RigidBody를 Unity에서 연결해줘야함

### 플레이어 동작

- 유저입력을 받아서, 플레이어가 힘을 받도록 (keyboard가 누른순간에 체크 함수가 동작해야함)
- 지속적으로 갱신을 받아야함 (update)
- Focus가 게임패널에 가야 동작이 된다

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
    public float speed = 10f;
    public Rigidbody playerRigidBody;

    // Start is called before the first frame update
    void Start()
    {
        playerRigidBody.AddForce(0, 1000, 0);
    }

    // Update is called once per frame
    void Update()
    {
        if(Input.GetKey(KeyCode.W))
        {
            playerRigidBody.AddForce(0, 0, speed);
        }
        if (Input.GetKey(KeyCode.A))
        {
            playerRigidBody.AddForce(-speed, 0, 0);
        }
        if (Input.GetKey(KeyCode.S))
        {
            playerRigidBody.AddForce(0, 0, -speed);
        }
        if (Input.GetKey(KeyCode.D))
        {
            playerRigidBody.AddForce(speed, 0, 0);
        }
    }

        void Update()
    {
        float inputX = Input.GetAxis("Horizontal");
        float inputZ = Input.GetAxis("Vertical");

        playerRigidBody.AddForce(inputX * speed, 0, inputZ * speed);
    }

}


public class Player : MonoBehaviour
{
    public float speed = 10f;
    private Rigidbody playerRigidBody;

    // Start is called before the first frame update
    void Start()
    {
        // 특정 타입에 대해, Game Object를 뒤져서 가져온다
        playerRigidBody = GetComponent<Rigidbody>();
        playerRigidBody.AddForce(0, 1000, 0);
    }

    // Update is called once per frame
    void Update()
    {
        float inputX = Input.GetAxis("Horizontal");
        float inputZ = Input.GetAxis("Vertical");

        // playerRigidBody.AddForce(inputX * speed, 0, inputZ * speed);

        float fallSpeed = playerRigidBody.velocity.y;

        Vector3 velocity = new Vector3(inputX, 0, inputZ);

        // (inputX * speed, 0 * speed, inputZ * speed)
        velocity = velocity * speed;

        velocity.y = fallSpeed;

        // (inputX * speed, fallSpeed, inputZ * speed)
        playerRigidBody.velocity = velocity;
    }
}
```
- // 발사 기능 - "fire" - 마우스 오른쪽 버튼 (custom 구현 가능)
- // 앉는 기능 - "Crunch" - 키보드 C
- // 점프 기능 - "Jump - 키보드 스페이스
- float inputX = Input.GetAxis("Horizontal");
  - 키보드 수평방향에 대응되는 키가 맵핑되있음 <- A  -1.0   0   + 1.0   ->  D (조이스틱은 살짝 미는거 구현 가능)
  - Edit/Project Settings/ Input Manager / Horizontal
- AddForce는 관성이 붙음, velocity는 바로 적용 가능 (Vector3 사용 - 추후 설명)
- GetComponent 사용

### 레벨 디자인

- cmd/ctrl 키 눌르면 grid 맞춰서 이동 가능
- 맵만들 때 사용 키 (마우스 오른쪽, 스크롤 키)
- 복사 cmd d
- scale과 position 값 수정
- Create Empty (이름지정: Level) Game Object 생성해서 hierarchy 정리
- 옮기려는 박스의 경우, 사이 간격보다 작게 해야함
- ItemBox에 RigidBody 설정
- 카메라 각도 설정
- Rigidbody - Freeze Position, Freeze Rotation
- 프리팹 만들기 (파일로서 미리 만드는 것) -> 재사용 가능한 게임 오브젝트 (Hierarchy에서 Asset으로 옮기기)
- scene 왼쪽 상단
  - pivot: 물체의 정해져있는 좌표의 기준 (default)
  - center: 눈으로 보이는 기준
  - global: 게임 세상을 기준으로 배치
  - local: 물체의 회전을 기준으로 배치
- Collider는 IsTrigger하면 물체의 충돌 감지하고, 물리적 표면이 사라짐
  - 특정 지점 도착시, 연출가능 (눈에 보이지않는 IsTrigger Collider 생성)
- 프리펩은 설정바꿔서 전체 apply 할 수 있다

### 오브젝트 회전 + 시간 간격
- 모든 게임 오브젝트는 transform component를 무조건 가지고 있음 (transform <- 사용 가능)
- Update함수 사용할 때, 시간 간격을 기준으로 작동하도록 (1초에 깜빡이는 횟수를 나누기 ) =
  - Time.deltaTime = 한 프레임의 시간 (화면을 60번 깜빡이면 초당 60프레임) 1/ 60, (화면을 200번 깜빡이면 200프레임) 1/ 200

### 충돌처리
- tag (game object를 분류하는 방법)
  - EndPoint 태그 추가
  - Add Component
- 충돌감지를 위해서는 OnTriggerEnter,OnCollisionEnter,OnTriggerExit,OnTriggerStay ...
-> unity가 자동으로 발동시켜주는 함수
```
void OnTriggerEnter(Collider other)
{
    if(other.tag == "EndPoint)
    {
        // do something
    }
}
// trigger와 collider가 부딫친다면
```
- Trigger인 클라이더와 충동할 때 자동으로 실행
- tag로 충돌대상 필터링 가능


```
void OnCollisionEnter(Colllider other)
{

}
```
- 일반 콜리이더와 충동했을 때 자동으로 실행

Mesh Renderer
```
private Renderer myRenderer;

private MyColor originalColor;

void Start()
{
    myRenderer = GetCOmponent<Renderer>();
    originalColor = myRendeer.
}
```
- `myRenderer.material.color = Color.red;`로 material 접근 가능

### 게임 매니저와 승리 조건
- 다른 Object에 isOverapped 추가
  - (script)에서 추rkehla
- Create Empty -> GameManager
- size 정하고 drag and drop

```
GameManager
public ItemBox itemBoxes;
public bool isGameOver;

void Start ()
{
    isGameOver = false;
}

void Update ()
{
    if(isGameOver == true)
    {
        return;
    }

    int count = 0;
    for( int i = 0; i < 3; i++)
    {
        if(itemBoxes[i].isOveraped == true)
        {
            count++;           
        }
    }
    if(count <= 3)
    {
        isGameOver = true;
    }
}
```

### 승리 UI 추가
- UI/Text 생성 (Hierarchy)
  - EventSystem (자동으로 유저입력입력을 UI에게 전달)
  - Canvas = 게임 패널의 크기 
    - 2D 모드 클릭하여 작업 가능 (Rect Transform - 사각형 영역에서의 transform)
    - Anchor Preset + Alt키
```
public GameObject winUI
winUI.SetActive(true);
```

- File/Build Seeting
  - Scenes In Build에 Main 추가
```
using UnitiyEngine.SceneManagement;

void Update ()
{
    if(Input.GetKeyDown(KeyCode.Space))
    {
        //SceneManager.LoadScene("Main");
        SceneManager.LoadScene(0);
    }
}
```
- 재시작 기능

