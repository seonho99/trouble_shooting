## Flutter Doctor CocoPods 오류 해결

3월 10일 부트캠프 시작하며, 그룹별로 공부한 내용을 공유하는 시간이 있었습니다.

부트캠프 처음 하신 분이 계셨고, 새 맥북에 `Android Stuido, Flutter` 설치가 안돼서

설치를 도와달라는 말에 설치를 도와드리게 되었습니다.

https://docs.flutter.dev/get-started/install/macos/mobile-ios

저는 맥북에 Flutter 설치는 4번 해봤으며, 공식 문서에 나와 있는 방법으로 진행 했습니다.

Android 버전을 설치를 했어야 했는데 iOS 버전을 다운받으셔서,

터미널에 `flutter doctor` 하니

```bash
✗ CocoaPods not installed.
        CocoaPods is a package manager for iOS or macOS platform code.
        Without CocoaPods, plugins will not work on iOS or macOS.
        For more info, see https://flutter.dev/to/platform-plugins
      For installation instructions, see
      https://guides.cocoapods.org/using/getting-started.html#installation
```

저는 iOS 했던 친구한테 `Cocoapods` 은 `Xcode`와 `iOS` 개발을 하기 위해 필요하다 라는 내용만 알았습니다.



```bash
GPT

CocoaPods는 iOS 및 macOS 개발에서 외부 라이브러리와 프레임워크의 종속성을 효율적으로 관리하기 위한 도구입니다. 
이를 통해 개발자는 필요한 라이브러리를 손쉽게 프로젝트에 추가하고 관리할 수 있습니다.

CocoaPods를 설치해야 하는 이유:

외부 라이브러리 관리: iOS 개발 시 다양한 기능을 구현하기 위해 외부 라이브러리를 사용하는데, 
CocoaPods는 이러한 라이브러리의 설치, 업데이트, 버전 관리를 간편하게 도와줍니다.

자동화된 설정: CocoaPods는 Xcode 프로젝트에 필요한 설정을 자동으로 구성해주어, 
개발자가 수동으로 설정할 필요를 줄여줍니다.

광범위한 라이브러리 지원: CocoaPods는 2024년 기준으로 10만 개 이상의 라이브러리를 지원하며,
전 세계적으로 3백만 개 이상의 앱에서 사용되고 있습니다. 

Ruby와 CocoaPods의 관계:

CocoaPods는 Ruby로 개발된 도구로, macOS에 기본적으로 설치되어 있는 Ruby 환경을 활용하여 작동합니다. 따라서 CocoaPods를 사용하려면 Ruby가 필요합니다.

구글링
CocoaPods
Swift 및 objective-c로 iOS / macOS 등 애플 플랫폼을 개발할 때, 
외부 라이브러리를 관리하기 쉽도록 도와주는 의존성 관리 도구의 일종입니다. 
그렇구만...
```

# 해결 과정

### **1️⃣** Xcode 설치 및 Xcode Apple ID 연동

### **2️⃣ Homebrew에 `Install Homebrew` 하단 명령어를 터미널에 입력**

https://brew.sh/ 링크

### 3️⃣ 터미널에 `sudo gem install cocoapods` 입력

https://guides.cocoapods.org/using/getting-started.html

```bash
설치 후 flutter doctor 확인해보니

ERROR:  Error installing cocoapods:
The last version of securerandom (>= 0.3) to support your Ruby & RubyGems was 0.3.2. Try installing it with

→ 오류: 코코아팟을 설치하는 동안 오류가 발생했습니다:
루비 및 루비젬을 지원하는 마지막 보안 랜덤 버전(>= 0.3)은 0.3.2입니다. 다음 버전으로 설치해 보세요.
```

### 여기서 에러 해결하는데 오래 걸렸습니다. 업그레이드 및 경로 지정 방법을 시도했지만 해결되지 않았고, 커니블로그를 통해 문제를 해결 할 수 있었습니다.

https://www.androidhuman.com/2021-04-18-flutter_cocoapods_not_installed_or_not_in_valid_state

### 선생님 감사합니다 🥹

```bash
터미널에서 uninstall 후 
sudo gem uninstall cocoapods
brew uninstall cocoapods

다시 install 하고 재부팅하니 오류를 해결할 수 있었습니다.
sudo gem install cocoapods
```