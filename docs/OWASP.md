# OWASP (보안취약점?)
> The Open Web Application Security Project
> 오픈소스 웹 애플리케이션 보안 프로젝트

## 공부자료
- [x] (wiki)[https://ko.wikipedia.org/wiki/OWASP]
- [x] (영상자료)[https://www.youtube.com/playlist?list=PLyqga7AXMtPPuibxp1N0TdyDrKwP9H_jD]

### 이건가?
- Injection (인젝션)
    - 동영상) login할 때, 로그인/pw말고, system command나 sql문을 보내서 데이터를 얻는 것
    - 해결책: user input이 들어올 때 **query parameterization**로 방지하는듯?
        - user input이 올 때, validation을 하는 것
        - DB에서는 LIMIT 1해줘서 certain amount만 보내게
        - 결론은 웹앱 잘 만들어라
    - wiki) SQL, OS, XXE(Xml eXternal Entity), LDAP 인젝션 취약점은 신뢰할 수 없는 데이터가 명령어나 쿼리문의 일부분으로써, 인터프리터로 보내질 때 발생한다. 공격자의 악의적인 데이터는 예상하지 못하는 명령을 실행하거나 적절한 권한 없이 데이터에 접근하도록 인터프리터를 속일 수 있다.

- Broken Authentication (취약한 인증) : bad guy에게 웹애플리케이션에 credential 없이 접속하게 해주는 것
    - 동영상) when log succeful, session id created. 
        - credential stuffing could happen! (다른 곳에서 훔친 know lists of id/pw로 웹사이트에 )
        - automated attacks: 랜덤하게 해보는 것
        - default password: admin/admin 
    - 해결책: 
        - multi factor auth(핸드폰등 2중 인증)
        - password checking: 쉬운 pw 다시 등록하라고 하는 것
        - password complexity: 처음에 어렵게 만들게
        - limit failed login: 여러번 시도 못하게
        - session management: 시간지나면 서버에서 new session id create하는 것 
    - wiki) 인증과 세션 관리와 관련된 애플리케이션 기능은 정확하게 구현되어 있지 않아서, 공격자가 패스워드, 키 또는 세션 토큰을 해킹하거나 다른 구현 취약점을 공격하여 다른 사용자 계정을 일시적 또는 영구적으로 탈취하는 것을 허용한다

- Sensitive Data Exposure (민감한 데이터 노출)
    - 동영상) 페이지에 여러개 있는데.. 
        - 몇개는 TLS or weak ciphers 몇개는 HTTP
        - 약한 곳 뚫고 민감한 데이터를 얻는듯
    - 해결책:
        - classify data: 중요한 데이터는  apply contorols
        - encrypt data at rest: 암호화 잘하기
        - strongn ciphers
        - possible PFS(perfect forward secrecy) or HSTS: strong form of TLS, HTTPS강제하기
        - sensitive data 저장하지 않기!(바로 지우기)
    - wiki) 많은 웹 애플리케이션들이 신용카드, 개인 식별 정보 및 인증 정보와 같은 중요한 데이터를 제대로 보호하지 않는다. 공격자는 신용카드 사기, 신분 도용 또는 다른 범죄를 수행하는 등 약하게 보호된 데이터를 훔치거나 변경할 수 있다. 중요 데이터가 저장 또는 전송 중이거나 브라우저와 교환하는 경우 특별히 주의하여야 하며, 암호화와 같은 보호조치를 취해야 한다.

- XML External Entities (XXE) (XML 외부 개체 (XXE))
    - 동영상) XML parser -> accept XML input directly: XML doc이 external entity를 갖고 있을 수 있음(bad payload(system command)같은거 보낼 수 있음)
    - 해결책:
        - disable 해야된다?
        - DTD processing?
        - soruce code analysis 
        - dyanamic application security test
        - webapp firewall
    - wiki) 오래되고 설정이 엉망인 많은 XML 프로세서들은 XML 문서 내에서 외부 개체 참조를 평가한다. 외부 개체는 파일 URI 처리기, 내부 파일 공유, 내부 포트 스캔, 원격 코드 실행과 서비스 거부공격을 사용하여 내부 파일을 공개하는데 사용할 수 있다.

- Broken Access Control (취약한 접근 통제)
    - 동영상) admin / normal user : 일반 유저가 admin access를 갖는 것
        - webapp.com/admin_info으로 접속하는 것
        - webapp./acctinfo?acct=1234로 접근
    - 해결책:
        - trusted access control code in server side
        - deny by default
        - log failiure 보내는 것
        - least previlidge: minimum access amount를 주는 것
    - wiki) 취약한 접근 제어는 인증된 사용자가 수행할 수 있는 것에 대한 제한이 제대로 적용되지 않는 것을 의미한다. 공격자는 이러한 취약점을 악용하여 사용자의 계정 액세스, 중요한 파일 보기, 사용자의 데이터 수정, 액세스 권한 변경 등과 같은 권한 없는 기능, 또는 데이터에 액세스할 수 있다.

- Security Misconfiguration (잘못된 보안 구성)
    - 동영상) 
        - default password사용
        - error message에 사용서버정보 제공 (해당 버전에 해당하는 vulnelability들이 있음)
        - default를 쓰고, update안해서.. 
        - security header를 사용해야함
    - 해결책
        - repeatable hardening process
        - all servers same config (update 다 하는 거 인듯?)
        - minimal platform: 서버동작에 필요한것만 사용
        - security directives: HSTS, HPKP, X-Frame-Options (security header)
    - wiki) 훌륭한 보안은 애플리케이션, 프레임워크, 애플리케이션 서버, 웹 서버, 데이터베이스 서버 및 플랫폼에 대해 보안 설정이 정의되고 적용되어 있다. 기본으로 제공되는 값은 종종 안전하지 않기 때문에 보안 설정은 정의, 구현 및 유지되어야 한다. 또한 소프트웨어는 최신의 상태로 유지해야 한다.

- Cross-Site Scripting (XSS) (크로스 사이트 스크립팅 (XSS))
    - 동영상)
        - POST <script>쿠키줘</script>
        - GET htttp://example.com/DBComment (latest DB comment 줘)
    - 해결책
        - firewall
    - wiki) XSS 취약점은 애플리케이션이 신뢰할 수 없는 데이터를 가져와 적절한 검증이나 제한 없이 웹 브라우저로 보낼 때 발생한다. XSS는 공격자가 피해자의 브라우저에 스크립트를 실행하여 사용자 세션 탈취, 웹 사이트 변조, 악의적인 사이트로 이동할 수 있다.

- Insecure Deserialization(안전하지 않은 역직렬화)
    - 동영상) object를 byte stream format으로 serialize하는 것 -> deserialize는 다시 object로
        - bad guy가 untrusted input으로 deserialize하는 것
        - cookie which includes userId: role: hash
        - Alice: Admin : 1234: xyz
    - 해결책
        - do not accept untrusted user input or validate it
    - wiki) 안전하지 않은 역직렬화는 종종 원격 코드 실행으로 이어집니다. 역직렬화 취약점이 원격 코드실행 결과를 가져오지 않더라도 이는 권한 상승 공격, 주입 공격과 재생 공격을 포함한 다양한 공격 수행에 사용될 수 있다.

- Using Components with Known Vulnerabilities (알려진 취약점이 있는 구성요소 사용)
    - 동영상) Apache/Oracle로 구성했는데, JavaVM이 vulnerable하거나.. 
        - vulnerable한 component를 사용 한 경우..
    - 해결책:
        - inventory clients/servers (계속 좋은거 찾기?)
        - download components from trusted source
        - plan monitor, patch, config
        - CVE, NVD (설명이 약하네 .?)
    - wiki) 컴포넌트, 라이브러리, 프레임워크 및 다른 소프트웨어 모듈은 대부분 항상 전체 권한으로 실행된다. 이러한 취약한 컴포넌트를 악용하여 공격하는 경우 심각한 데이터 손실이 발생하거나 서버가 장악된다. 알려진 취약점이 있는 컴포넌트를 사용하는 애플리케이션은 애플리케이션 방어 체계를 손상하거나, 공격 가능한 범위를 활성화하는 등의 영향을 미친다.

- Insufficient Logging & Monitoring(불충분한 로깅 및 모니터링)
    - 동영상) log를 찍고, log를 monitoring
        - failed login/ warnings/ error msgs/ alert thresholds
        - log file 노출하지 않기
    - 해결책
        - 이상한 로그 찾기
        - sufficient content(로그내용을 알아볼 수 있을 정도로)
        - good format ( logging service로 만들기 편한 형태로)
        - too much or too little! needs balance
        - integrity controls(불변함)
        - response plan (문제 생겼을 떄 뭐할지 plan)
    - wiki) 불충분한 로깅과 모니터링은 사고 대응의 비효율적인 통합 또는 누락과 함께 공격자들이 시스템을 더 공격하고, 지속성을 유지하며, 더 많은 시스템을 중심으로 공격할 수 있도록 만들고, 데이터를 변조, 추출 또는 파괴할 수 있다. 대부분의 침해 사례에서 침해를 탐지하는 시간이 200일이 넘게 걸리는 것을 보여주고, 이는 일반적으로 내부 프로세스와 모니터링보다 외부기관이 탐지한다.

1.XSS
2.Injection Flaws
3.악성 파일 실행
4.불안전한 직접 객체 참조
5.Cross-Site Request Forgery
6.정보유출 및 부적절한 오류
7.취약한 인증 및 세션 관리
8.불안전한 암호화 저장
9.불안전한 통신
10.URL 접속 제한 실패
