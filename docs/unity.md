# unity

## 개요/목표
- 사이드 프로젝트를 위한 유니티 공부

## 공부자료
- 강의
- [x] [retr0의 유니티](https://www.udemy.com/course/retr0-unity/)
- [ ] [인프런](https://www.inflearn.com/course/mmorpg-%EC%9C%A0%EB%8B%88%ED%8B%B0)

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

### 최종 빌드
- Add Component (Audio Source)
- 끝날 때 Player 못 움직이게
  - GameManager 오브젝트 가져와서, 조건 확인하고 Update에서 early return

- Build And Run으로 저장 (프로젝트의 경로에 저장하지 않기)

### 평행이동과 좌표게
```
Vector3 targetPosition = new Vector3(1,0,0);
transform.position = targetPosition;

transform.Translate(targetPosition);
``` 
- transform은 해당 object의 transform

`transform.Translate(move * Time.deltaTime, Space.World or Space.Self)`
- local space - 부모와 나 (상대적) -> 자신의 기준으로
- global space - 게임계와 나 (절대적) -> 게임세상을 기준으로
- localPosition/position..

### 회전가 쿼터니언
- 90도 회전하면... gimbal_lock
  - Quaternion이 필요
```
Qutaernion.Euler(new Vector3(30,45,60))

Vector3 direction = targetTransform.position - trnasform.position;

Quaternion targetRotation = Quarternion.LookRotation(direction);

transform.rotation = targetRotation;

```
- z축이 앞면
- Lerp는 중간지대 Quaternion.Lerp(aRotation,bRoation,0.5f)
- 쿼터니언을 vector로 쿼터니언.eulerAngles;

### 인스턴스화
- 미리 만들어진 게임 오브젝트를 게임 도중에 필요한만큼 찍어내는 것
  - Instantiate에 타겟 넘겨서 (target,위치,회전)
- 프리펩을 등록해놓고 생성 (총알, 몬스터, etc...)

### 코루틴
- 처리와 처리사이에 대기시간 삽입, 여러처리를 동시에 병렬처리
- fade-in, fade-out 구현할 때
- async
- coroutine 함수 넣으면 성능이 더 좋음, string으로 넣으면, 중간에 stop 가능
- yield null값은 1frame

### 레이 케스트
- 물체에서 나온 광선이 닿는 곳이 있는지 확인 가능
- DrawRay로 광선 확인 가능
- RaycastHit

## 인프런 유니티 강좌
## 개론
### 환경 설정
- window/layouts/tall
  - game을 scene 밑으로, console은 inspector 밑으로
- scene을 여러개 생성해서, 로그인 창, 로비창 등으로 만들어 줄 수 있음
 
## 유니티 기초
### 에디터 입문
- Scene: 영화 세트 촬영장
  - 배우, 소품을 배치하고 카메라로 찍는 것
- Hierarchy: 
  - Game Object
  - Directional Light: 조명
  - Main Camera: 영화에서 카메라 (삼각형 안이 화면에 보이는 것)
- 사용자는 촬영장(Scene)안을 마음껏 돌아다니는 것이 아닌 Main Camera로 찍은 것을 볼 수 있는 것
- Project:
  - 영화 찍기위한 모든 소품을 넣는 것
  - Asset: 영화에서 촬영할 배우, 옷, 소품, 음악 등을 넣음 (실제로 영화에 등장하는 것이 아님, 등장을 원하면 Hierarchy에 배치필요)
- Inspector: 촬영장의 각 물품에 대한 상세 설명을 나타냄
- 움직임
  - 마우스 오른쪽 누르고 WASD 눌러서 움직일 수 있음
  - 마우스 오른쪽 누르고 QE 눌러서 위아래 움직일 수 있음
  - alt key 누르고 마우스 우클릭, 위아래 하면 확대 축소 가능
  - alt key 누르고 마우스 왼쪽, 주시하는 기반으로 이동 가능
  - 마우스 휠로 확대 축소 가능
  - 마우스 오른쪽 누르고 휠로 가상 카메라 속도 조절 가능
  - 물제 선택하고 Q,W(move tool),E(rotate tool),R(scale tool)
    - tranform 정보가 변함
- ctrl shift f 하면 영화감독이 위치한 곳으로 카메라가 위치함

### Play
- 클라이언트 개발은 영화 촬영, 서버는 식당 운영
  - Scene은 실제 촬영을 하는 세트장
  - Game은 카메라로 보여주는 화면
- 영화와 게임의 차이
  - 영화는 녹화하여 보여주고, 게임은 실시간 촬영을 보여주는 것
  - 게임에서는 촬영하는 장본인이 플레이어 자신
  - FPS는 플레이어 머리 눈 위에 카메라 위치
  - 디아블로는 탑뷰로 플레이어 위에 카메라 위치
- 플레이 버튼을 통해 촬영 가능 (ctrl p)
  - 촬영이 시작된 이후의 행동들은 기억되지않고 촬영이 종료되는 순간 날라감 (play button을 누르고 작업하면 다 날아가니 주의)

### Component 패턴
- 코드를 부품화하여 관리
- empty game object에 부품(컴포넌트)을 가져다 붙혀서 새로운 것을 만듦
- C# 파일도 컴포넌트
  - Start()는 최초 한번 호출되는 것
  - Update() tick마다 계속 호출

### 매니저 만들기
- Project의 뼈대가되는 매니저
  - Tip: Component 용도로 사용될 c#파일과 일반적인 c#파일을 구분
- 전역에서 사용가능한 매니저를 만들어서 어디서든 사용가능 하도록
- MonoBehaviour를 상속받아야 유니티 툴에서 컴포넌트로서 사용가능
- 일반적인 C#파일로 사용하려면 MonoBehaviour의 상속 구조를 제거한다면..
  - 하지만, 해당 파일의 Start와 Update함수가 유니티에서 호출되지 않음
  - Tip: scene에 배치하는 게임 오브젝트는 꼭 실체가 있는 사물일 필요는 없다 
  - -> 코드를 뒷받침하는 매니저를 빈 게임 오브젝트에 넣어서 붙혀도 됨
- @Managers <- convention상 @는 지우면 안된다는 것 (추가기능 x)
- Scripts 폴더 생성
  - Scripts/Managers

### Singleton 패턴
- Managers는 어디서든 편하게 갖고와서 사용할 수 있는 클래스로서 만들예정
- Managers를 어떻게 가져올 수 있을까?
  - Unity GUI에서 drag/drop 및 UI 만드는 기능은 코드상으로 다 가능
  - ex) Hierarchy안의 @Managers를 찾는 기능도 있을것임
    - `GameObject go = GameObject.Find("@Managers");Managers mg = go.GetComponent<Managers>();`
    - 하지만 비효율적
- Managers는 하나만 존재햇으면 함
- DontDestroyOnLoad - 안전보장
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Managers : MonoBehaviour
{
    static Managers s_instance; // 유일성이 보장
    public static Managers Instance { get { Init(); return s_instance; } } // 유일한 매니저를 갖고온

    // Start is called before the first frame update
    void Start()
    {
        Init();
    }

    // Update is called once per frame
    void Update()
    {
        
    }

    static void Init()
    {
        if (s_instance == null)
        {
            GameObject go = GameObject.Find("@Managers");
            if (go == null)
            {
                go = new GameObject { name = "@Managers" };
                go.AddComponent<Managers>();
            }

            DontDestroyOnLoad(go);
            s_instance = go.GetComponent<Managers>();
        }
    }
}
```

## Transform
### 플레이어 설정
- Unity Store
  - Models: 대표 배우
  - Materials: 의상, 재질 (빛을 반사해서 어떻게 보여질지)
    - find reference scene에서 어디에서 사용되는지 볼 수 있음
  - Animations: 여러가지 모션
  - 예시로 받은 unity-chan도 각각의 컴포넌트로 조립해서 만들어진 것 (prefab으로 관리되는 것)
- 움직임을 대상하려는 GameObject의 transform.position을 Input.GetKey에 맞게 바꿔주도록 함

### Position
- Update는 1frame마다 발생 - ex) 60Frame이라면 1/60초 마다 이동을 하는 것
  - 이전 frame과 현재 frame의 시간차를 구해서 이동하도록
    - Time.deltaTime * _speed
  - [SerializeField] -> C# reflection
- Transform Component
  - Position: 필드의 좌표에 배치
  - Rotation: Degree 회전
  - Scale: 각 축으로 해당 GameObject가 확대/축소
- 게임 세상의 world 좌표, Player의 local 좌표
  - x 누르면 local 좌표를 볼 수 있음
    - local좌표는 아트, 모델러들이 사용하는 좌표계
```
// Local -> World 
// transform.TransformDirection()

// World -> Local
// transform.InverseTransformDirection()
```
- transform.Translate 사용하면 현재바라보고 있는 ㅣocal을 기준으로 이동

### Vector3
- 위치 벡터
- 방향 벡터
  - 방향값과 방향의 크기를 나타냄
  - to - from를 빼면 방향을 나타낼 수 있음 (목적지에서 현재위치 뺀 것)
  - 거리(크기)와 실제 방향을 얻을 수 있음
  - magnitude (거리)
    - mathf.sqrt(x*x + y*y + z*z)
  - normalized (실제 방향)
      - new Vector (x / magnitude, y / magnitude, z / magnitude)
      - 단위 벡터, 단위가 1짜리
```
MyVector to = new Vector(..., ..., ...);
MyVector from = new Vector(..., ..., ...);
MyVector dir = to - from;

dir = dir.normalized;

MyVecotr newPos = from + dir * _speed;
```
- 벡터는 float 셰개를 들고있는 구조체이다. 위치 또는 방향으로 사용가능.
  - 두 벡터의 뺄셈을 이용하여 방향 벡터 추출
    - 방향 벡터는 거리와 실제 방향 정보를 담고있음 (magnitude로 거리 추출, normalized롤 실제 방향 추출)
      - normalized로 방향은 같지만 크기가 1인 벡터 추출

### Rotation
- transform.eulerAngles = new Vector(..., ..., ...,)
- eulerAngles보다는 transform.Rotate(new Vector(..., ..., ...,)) 사용 권장
  - world,local 기준 설정 가능
- transform.rotation
- Quaternion은 x,y,z,w
  - gimbal lock문제로 quaternion을 사용
- Quaternion.Slerp(, , 0.0 ~ 1)
- -> 다시 한번 정리하면 좋을듯!

### Input Manager
- InputManager를 Managers에 추가

## 프리팹 (Pre-Fabrication)
### Prefab #1
- 컴포넌트 산하관계로 만들면 같이 이동
- 프리팹은 붕어빵 틀 같은 것 (클래스와 인스턴스 관계와 비슷)
  - 프리팹에 적용된 값이 해당 프리팹으로 생성된 인스턴스들이 같은 값을 갖게됨
- 프리팹 더블 클릭하여 프리팹모드에서 프리팹 수정 가능

### Prefab #2
- prefab override한 값은 값이 안바뀜
- Nested Prefab
  - 포함 관계
- Prefab Variant
  - 기존 프리팹을 상속받은 프리팹

### Resource Manager
- prefab = Resources.Load<GameObject>("Prefabs/Tank");
  - Resources 폴더 밑에

## Collision
### Collider
- RigidBody
  - 어떤 물체의 포지션을 물리적인 시뮬레이션의 영향을 줘서 컨트롤
  - RigidBody를 붙히면 Unity의 물리엔진의 영향을 받는다
- 두 물체 다 Collider가 있어야함

### Collision
- RigidBody에서 Freeze Rotation x,y,z 해서 안 넘어지도록 할 수 있음
- `OnCollisionEnter`
  - 나한테 혹은 상대에게 RigidBody가 있어야함 (IsKinematic : Off)
  - 나한테 Collider가 있어야함 (IsTrigger : Off)
  - 상대한테 Collider가 있어야함 (IsTrigger : Off)
- IsKinematic사용하면 유니티 물리엔진 영향 받지 않음

### Trigger
- Collision시 IsTrigger 세팅되어있으면 OnTriggerEnter 이벤트 발생
- 스킬, 몬스터 타격을 통해 공격했을 때 데미지
- 투명 cube안에 도착했을 때 던전 순간이동 장치로

### Raycasting #1
- 클릭했을 때 선택되는 것
- 레이저로 포인터 쏘는 것
- 카메라에서 2d좌표를 눌렀을 때 캐릭터를 찍는 것
- `Physics.Raycast`, `Debug.DrawRay`
- 첫번째 물체만 관통
  - `Physics.RaycastAll` 사용하면 모두 관통
- 카메라 벽에 가려졌을 때, 플레이어에서 카메라로 Raycast되는곳으로 카메라를 옮김

### 투영의 개념 + Raycasting #2
- // Local <-> World <-> Viewport <-> Screen
- 카메라 영역을 벗어나면, 연산하지 않음
-> 3d에서 2d로 넘어올 때 좌표값이 하나 없어짐
-> 카메라에서는 무조건 비율이 맞게 들어감

```
if (Input.GetMouseButtonDown(0))
{
  //Input.mousePosition // Screen (픽셀좌표)
  //Camera.main.ScreenToViewportPoint(Input.mousePosition) // Viewport (특정 픽셀의 비율의 좌표


  Vector3 mousePos = Camera.main.ScreenToWorlPoint(new Vector3(Input.mousePosition.X, Input.mousePosition.Y, Camera.main.nearClipPlane));
  Vector3 dir = mousePos - Camera.main.tranform.position;
  dir = dir.normalized;

  Debug.DrawRay(Camera.main.transform.position, dir * 100.0f, Color.red, 1.0f);

  RaycastHit hit;
  if (Physics.Raycast(Camera.main.transform.position, dir, out hit, 100.0f))
  {
    Debug.Log($"Raycast Camera @ {hit.collider.gameObject.name}");
  }
}
```
`Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);`

### LayerMask
- Mesh Collider의 충돌 범위를 인식해야할 경우, 연산부하가 많음
  - 최적화를 충돌전용 Mesh를 하나 더 만듦
- 모든 object를 대상으로 Raycasting하면 연산량이 많아짐
  - AddLayer해서 전용 Layer 생성
    - 0 ~ 31의 bitflag

## Camera
- 카메라가 플레이어를 따라가도록
```
public class CameraController : MonoBehaviour
{
    [SerializeField]
    Define.CameraMode _mode = Define.CameraMode.QuarterView;

    [SerializeField]
    Vector3 _delta = new Vector3(0.0f, 6.0f, -5.0f);

    [SerializeField]
    GameObject _player = null;

    void LateUpdate()
    {
        RaycastHit hit;
        if (Physics.Raycast(_player.transform.position, _delta, out hit, _delta.magnitude, LayerMask.GetMask("Wall")))
        {
            float dist = (hit.point - _player.transform.position).magnitude * 0.8f;
            transform.position = _player.transform.position + _delta.normalized * dist;
        }
        else
        {
            transform.position = _player.transform.position + _delta;
            transform.LookAt(_player.transform);
        }
    }

    public void SetOuterView(Vector3 delta)
    {
        _mode = Define.CameraMode.QuarterView;
        _delta = delta;
    }
}
```

## Animation
### Animation 기초
- humonoid 모델
- Animation Component는 legacy
- Animator Component를 사용
  - alt key, scroll key 누르고 움직일 수 있음
- 애니메이션은 짧은 동영상 캡처파일
  - animator는 영화 재생기 같은 느낌
- entry에 set statemachie default state

### Animation Blending
- 게임에서는 급하게 멈추는것을 좋아하지 않음
- Blending을 사용하여 서서히 State를 변화하도록 할 수 있음
```
if (_moveToDest)
{
    wait_run_ratio = Mathf.Lerp(wait_run_ratio, 1, 10.0f * Time.deltaTime);
    Animator anim = GetComponent<Animator>();
    anim.SetFloat("wait_run_ratio", wait_run_ratio);
    anim.Play("WAIT_RUN");
}
else
{
    wait_run_ratio = Mathf.Lerp(wait_run_ratio, 0, 10.0f * Time.deltaTime);
    Animator anim = GetComponent<Animator>();
    anim.SetFloat("wait_run_ratio", wait_run_ratio);
    anim.Play("WAIT_RUN");
}
```

### State 패턴
- 직접 blending을 위의 예제처럼 다 맞춰줘야하는 것인가?
```

### State Machine

