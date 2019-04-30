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
