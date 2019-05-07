# react-native-firebase

기본세팅
```
import firebase from 'firebase';
import { firebaseConfig } from './config';
firebase.initializeApp(firebaseConfig);
```

loading화면에서 로그인 확인 (react-native navigtaion사용 경우)
```
componentDidMount() {
    this.checkedIfLoggedIn();
}

checkedIfLoggedIn = () => {
    firebase.auth().onAuthStateChanged((user) => {
    if(user) {
        this.props.navigation.navigate('DashboardScreen');
    }
    else {
        this.props.navigation.navigate('LoginScreen');
        //this.props.navigation.navigate('DashboardScreen');
    }
    })
}
```

Authentication 설정을 선택하여 로그인 및 회원가입 방법 설정
```
  signupUser = (email, password) => {
    firebase.auth().createUserWithEmailAndPassword(email, password).catch(function(error) {
      // Handle Errors here.
      var errorCode = error.code;
      var errorMessage = error.message;
      // [START_EXCLUDE]
      if (errorCode == 'auth/weak-password') {
        alert('The password is too weak.');
      } else {
        alert(errorMessage);
      }
      console.log(error);
      // [END_EXCLUDE]
    });
  }
```

## add data to real-time database(signup)

실시간 데이터베이스
- 데이터를 하나의 큰 JSON 트리로 지정합니다.
- 사용자 ID 또는 의미를 가진 이름과 같은 고유 키로 직접 지정할 수도 있고, push()를 사용하여 자동으로 지정할 수도 있습니다.
[https://stackoverflow.com/questions/38800079/cannot-add-node-to-firebase-through-console][add node to firebase]

## User property

사용자 속성
- Firebase User에는 고정된 기본 속성 집합(고유 ID, 기본 이메일 주소, 이름, 사진 URL)이 있습니다. 이러한 속성은 프로젝트의 사용자 데이터베이스에 저장되며 사용자가 업데이트할 수 있습니다(iOS, Android, 웹). Firebase User 객체에 직접 다른 속성을 추가할 수는 없으며 대신 추가 속성을 Google Cloud Firestore와 같은 다른 저장소 서비스에 저장할 수 있습니다.
사용자가 앱에 처음 가입할 때, 사용 가능한 다음 정보를 토대로 사용자의 프로필 데이터가 채워집니다.
- 사용자가 이메일 주소와 비밀번호로 가입했다면 기본 이메일 주소 속성만 채웁니다.
- 사용자가 Google 또는 Facebook 등의 제휴 ID 제공업체를 사용해 가입했다면 업체에서 제공하는 계정 정보를 가져와 Firebase User의 프로필을 채웁니다.
- 사용자가 맞춤 인증 시스템으로 가입했다면 원하는 정보를 Firebase User의 프로필에 명시적으로 추가해야 합니다.

## user reload
이메일 인증을 하고난 후, 바로 현재 signin되어 있는 user의 emailVerified가 true값으로 변환되지 않는다. 해당 문제를 해결하기 위해 user.reload()를 호출하여 emailVerified를 확인해야한다.
```
    checkVerification = () => {
        firebase.auth().onAuthStateChanged((user) => {
            user.reload().then(() => {
                if(user.emailVerified) {
                    this.props.navigation.navigate('DashboardScreen');
                  }
                  else {
                    //do nothing
                  }
            });

          })
    }
```
- then()을 사용하지 않는 경우, 동시다발적으로 코드가 실행되여 제 때 emailVerified를 확인하지 못할 수 있다.