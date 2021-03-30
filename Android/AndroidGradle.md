# Android와 Gradle

## 빌드 프로세스

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c109ba58-db70-4f6b-98ff-b0cb0e2a3ae2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c109ba58-db70-4f6b-98ff-b0cb0e2a3ae2/Untitled.png)

1. 컴파일러는 소스 코드를 DEX(Dalvik Executable) 파일로 변환하고 그 외 모든 것은 컴파일된 리소스로 변환합니다. 이 DEX 파일에는 Android 기기에서 실행되는 바이트 코드가 포함됩니다.
2. APK Packager는 DEX 파일과 컴파일된 리소스를 단일 APK로 결합합니다. 그러나, 앱을 Android 기기에 설치하고 배포할 수 있으려면 먼저 APK에 서명해야 합니다.
3. APK Packager는 디버그 또는 출시 키 저장소를 사용하여 APK에 서명합니다.
    1. 디버그 버전의 앱(즉, 테스트 및 프로파일링 전용 앱)을 빌드 중인 경우에는 패키저가 디버그 키 저장소로 앱에 서명합니다. Android 스튜디오는 디버그 키 저장소로 새 프로젝트를 자동으로 구성합니다.
    2. 출시 버전의 앱(즉, 외부에 출시할 앱)을 빌드 중인 경우에는 패키저가 출시 키 저장소로 앱에 서명합니다. 출시 키 저장소를 생성하려면 [Android 스튜디오의 앱 서명](https://developer.android.com/studio/publish/app-signing#studio)을 참고하세요.
4. 최종 APK를 생성하기 전에, 패키저는 앱이 기기에서 실행될 때 더 적은 메모리를 사용하도록 앱을 최적화하기 위해 [zipalign](https://developer.android.com/studio/command-line/zipalign) 도구를 사용합니다.

### settings.gradle

앱 빌드 시 포함해야 하는 모듈을 알려줌

### build.gradle 프로젝트

프로젝트의 모든 모듈에 적용되는 빌드 구성 정의

dependency 정의

### build.gradle 앱

앱의 빌드 구성 설정

앱 모듈이 반드시 알아야 할 것들 정의

### gradle.properties

gradle 설정, 최대 힙 크기

### local.properties

로컬 환경 구성

sdk경로 cmake 경로
