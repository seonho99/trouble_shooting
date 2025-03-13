<img width="560" alt="Image" src="https://github.com/user-attachments/assets/50ff1b0c-0bb0-4e1c-a123-ce1a0675bee4" />

# Flutter Upgrade를 했습니다.
선생님의 과제 제출 폴더를 GitHub에서 Fork를 하고 제 Dart SDK를 연동했더니
선생님의 Dart SDK는 3.7 version 이였고, 저는 3.6 version 이였습니다.

<img width="709" alt="Image" src="https://github.com/user-attachments/assets/27665962-e0eb-4ea2-8581-615a8dd00e7d" />

Flutter Upgrade 를 안하면 돼지 않냐?

→ 과제 또는 팀 플젝 기간일 때 같은 개발환경에서 개발을 해야 할 수 있으므로
업그레이드를 해야 될 가능성이 큽니다.

그렇다면 Flutter Upgrade를 해라!

→ 개인 앱이 Dart 3.6 version 입니다…
→ 새싹 스승님께서 Flutter Upgrade는 라이브러리 버전이 오래되어 동작하지 않을 때,
동작하지 않는 라이브러리 하나씩 업그레이드하는게 좋다. 말씀하셨습니다.

### 결과적으로

매도 일찍 맞는 매가 덜 아프다고,
시간이 조금 널널한 지금 업그레이드 하는 편이 좋다고 판단 했습니다.

<img width="732" alt="Image" src="https://github.com/user-attachments/assets/8e5e6989-f93b-4d40-b564-ffe5189464e5" />

터미널에서 `Flutter upgrade`를 하고
Android Studio 에서 SDK 버전 확인

<img width="1055" alt="Image" src="https://github.com/user-attachments/assets/75750bff-4d36-4b6e-b063-85ea002ee501" />


버전도 3.7 최신이니 이제 저의 개인 앱을 한번 보겠습니다.
`pubspec.yaml` 도 `Pub upgrade` 해주고… 가보자!!!

<img width="1281" alt="Image" src="https://github.com/user-attachments/assets/1c79c2c6-2041-4faf-aba9-9bfae8b34247" />

… 역시나 콘솔창은
```bash
Error: The pod "Firebase/Storage" required by the plugin "firebase_storage" requires a higher minimum ioS deployment version than the plugin's reported minimum sversion.
To build, remove the plugin "firebase_storage", or contact the plugin's developers for assistance.
Error running pod install
Error launching application on iPhone 16.

-> 오류: 플러그인 “firebase_storage”에 필요한 “Firebase/Storage” 파드에 플러그인의 보고된 최소 버전보다 더 높은 최소 ioS 배포 버전이 필요합니다.
빌드하려면 플러그인 “firebase_storage”를 제거하거나 플러그인 개발자에게 도움을 요청하세요.
포드 설치 실행 중 오류 발생
iPhone 16에서 애플리케이션을 실행하는 동안 오류가 발생했습니다.
```

어제도 그렇고 `CocoaPads` 이놈 참 까다롭습니다. 아니지 `iOS`가 까다로운건가…?

## 해결 과정

### 1️⃣ Xcode 코드를 들어가서 버전 확인 후 높은 버전으로 올렸습니다.

<img width="1126" alt="Image" src="https://github.com/user-attachments/assets/c3c89917-4bab-433f-a893-5e7c6eb8ef02" />

### 2️⃣ 어제 `flutter doctor`에 `uninstall`이 생각나서 `uninstall` → `install` 했습니다.

<img width="669" alt="Image" src="https://github.com/user-attachments/assets/a50d6986-48cf-4da9-b52a-8c5964562412" />

<img width="670" alt="Image" src="https://github.com/user-attachments/assets/00ce246c-4c8d-4923-a60c-156222cd265c" />

### 그 후에도 Android Studio 는 동일한 에러가 나와, GPT 한테 물어보니 `Pods` 전부 지우고 다시 설치하라고 해서 진행 했습니다.

<img width="938" alt="Image" src="https://github.com/user-attachments/assets/bf64a24e-4fa5-4796-a6ba-1d1b1a6932c0" />

```bash
rm -rf Pods
rm -f Pdofile.lock
rm -rf ~/Library/Developer/Xcode/DerivedData/*
pod cache clean --all
pod install
```

### 리눅스 강의에서 `rm -rf`는 강제로 파일을 삭제하는 명령어라 함부로 사용하지 말라고 배웠지만, 두 번 `Pods` 파일을 삭제하고 `pod install` 해서 Android Studio가 정상적으로 작동했던 경험이 있어서 진행 했습니다.

<img width="1361" alt="Image" src="https://github.com/user-attachments/assets/fa2e9679-fb85-432c-bbe2-ee4f56fef1d5" />

```bash
[!] CocoaPods did not set the base configuration of your project
because your project already has a custom config set.
In order for CocoaPods integration to work at all,
please either set the base configurations of the target 'Runner' to
'Target Support Files/Pods-Runner/Pods-Runner profile xcconfig' or include the
'Target Support Files
/Pods-Runner/Pods-Runner profile xcconfig' in your build configuration ('Flutter/Release.cconfig*).

-> [프로젝트에 이미 사용자 지정 구성이 설정되어 있기 때문에 CocoaPods가 프로젝트의 기본 구성을 설정하지 않았습니다.
CocoaPods 통합이 제대로 작동하려면 대상 'Runner'의 기본 구성을 '대상 지원 파일/팟-러너/팟-러너 프로파일 xcconfig'로 설정하거나,
'대상 지원 파일/팟-러너'의 기본 구성에
'타겟 지원 파일
/Pods-Runner/Pods-Runner 프로파일 xcconfig'를 빌드 구성('Flutter/Release.cconfig*')에 포함하세요.
```

<img width="1466" alt="Image" src="https://github.com/user-attachments/assets/a89371e4-d8a0-44c9-b610-3d703fed0682" />


### Xcode 열어서 /Pods-Runner/Pods-Runner 최신으로 올려주고
### 재 앱을 실행시켰더니 앱이 정상적으로 나옵니다 !!

<img width="917" alt="Image" src="https://github.com/user-attachments/assets/41c87c01-f57a-414e-92ce-fa2167eabd54" />

### `git push` 까지

<img width="739" alt="Image" src="https://github.com/user-attachments/assets/d096d324-5c25-4861-b20f-2fe6064eac17" />