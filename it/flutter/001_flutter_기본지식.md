### 📌 **Flutter 기본 지식 정리**  

Flutter는 Google이 개발한 **오픈 소스 UI 프레임워크**로, **iOS, Android, 웹, 데스크톱**에서 동일한 코드베이스로 실행되는 애플리케이션을 만들 수 있습니다.  

---  

## 1️⃣ **Flutter란?**
- **크로스 플랫폼 프레임워크**: 하나의 코드로 여러 플랫폼(iOS, Android, 웹, 데스크톱)에서 실행  
- **Dart 언어 사용**: 빠른 개발 속도를 위해 Google이 개발한 Dart 프로그래밍 언어 사용  
- **위젯 기반 UI**: Flutter의 모든 요소(UI)는 **위젯**(Widget)으로 구성됨  
- **고성능 프레임워크**: 네이티브 성능과 가까운 속도를 제공  

---

## 2️⃣ **Flutter의 주요 특징**
### ✅ **1. 위젯 기반 UI**  
- Flutter에서 UI 요소들은 모두 **위젯(Widget)**으로 구성  
- 위젯은 작은 단위의 UI 요소이며, 이를 조합하여 화면을 구성  

👉 예시)  
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter 기본 예제')),
        body: Center(child: Text('Hello, Flutter!')),
      ),
    );
  }
}
```

---

### ✅ **2. 핫 리로드(Hot Reload)**
- 코드 수정 후 앱을 다시 실행하지 않고 즉시 반영  
- UI 및 로직 변경 사항을 실시간으로 확인 가능  

---

### ✅ **3. 단일 코드베이스**
- 한 번의 코드 작성으로 **iOS, Android, 웹, 데스크톱**에서 실행 가능  
- 네이티브 UI와 유사한 디자인 및 성능 제공  

---

### ✅ **4. 높은 성능**
- **Skia 그래픽 엔진** 사용  
- 네이티브 브릿지를 최소화하여 빠른 렌더링 가능  

---

## 3️⃣ **Flutter 기본 구조**
Flutter 프로젝트는 기본적으로 다음과 같은 디렉토리 구조를 가집니다.  

```
my_flutter_project/
 ├── lib/                 # Dart 코드 (앱의 핵심 코드)
 │   ├── main.dart        # 앱의 진입점
 ├── android/             # 안드로이드 네이티브 코드
 ├── ios/                 # iOS 네이티브 코드
 ├── web/                 # 웹 관련 파일
 ├── test/                # 테스트 코드
 ├── pubspec.yaml         # 프로젝트 설정 파일 (패키지, 의존성 등)
 └── README.md            # 프로젝트 설명
```

### 🔹 **main.dart 파일의 기본 구조**
```dart
void main() {
  runApp(MyApp()); // 앱 실행
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter 앱')),
        body: Center(child: Text('Hello, Flutter!')),
      ),
    );
  }
}
```

---

## 4️⃣ **Flutter 주요 위젯**
Flutter에서 UI는 다양한 위젯을 조합하여 구성됩니다.

### 🎨 **기본 위젯**
- **Text**: 텍스트 표시 (`Text("Hello, Flutter")`)
- **Container**: 박스 형태의 UI 요소 (`Container(width: 100, height: 100, color: Colors.blue)`)
- **Row & Column**: 수평(`Row`) / 수직(`Column`) 레이아웃 구성
- **Image**: 이미지 표시 (`Image.network("https://example.com/image.png")`)
- **Button**: 버튼 (`ElevatedButton(onPressed: () {}, child: Text("클릭"))`)

---

## 5️⃣ **Flutter 앱 개발 흐름**
1. **Flutter 설치 및 환경 설정**  
   - Flutter SDK 설치  
   - Android Studio 또는 Visual Studio Code 설정  
   - `flutter doctor` 명령어로 환경 확인  

2. **Flutter 프로젝트 생성**
   ```
   flutter create my_app
   cd my_app
   flutter run
   ```

3. **앱 개발** (UI 구성, 기능 구현)  
4. **디버깅 및 테스트**  
5. **앱 빌드 및 배포** (Android/iOS 스토어 업로드)  

---

## 6️⃣ **Flutter 패키지 활용**
Flutter에서는 다양한 **패키지**를 통해 기능을 확장할 수 있습니다.  

**📦 패키지 추가 방법 (pubspec.yaml)**  
```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  http: ^0.13.4  # HTTP 요청 라이브러리
```
👉 패키지 설치  
```
flutter pub get
```

**🎯 유용한 패키지**
- `http`: REST API 요청
- `provider`: 상태 관리
- `shared_preferences`: 로컬 저장소 활용
- `url_launcher`: 웹 URL 열기
- `firebase_core`: Firebase 연동

---

## 🔥 **정리**
| 개념 | 설명 |
|------|------|
| UI 구조 | **위젯 기반** (StatelessWidget / StatefulWidget) |
| 개발 속도 | **핫 리로드(Hot Reload)** 지원 |
| 성능 | **네이티브 성능**에 가까운 속도 |
| 언어 | **Dart 프로그래밍 언어** 사용 |
| 코드 공유 | **iOS, Android, 웹, 데스크톱**에서 동작 |

---

### 🚀 **Flutter를 배우고 싶다면?**
- 공식 문서: [https://flutter.dev](https://flutter.dev)  
- 패키지 검색: [https://pub.dev](https://pub.dev)  
- 예제 코드: [https://flutterawesome.com](https://flutterawesome.com)  
