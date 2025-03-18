## 📌 **Flutter에서 사이드바(Side Navigation Drawer) 사용 방법**  

Flutter에서 **사이드바(Side Navigation Drawer)**는 `Drawer` 위젯을 사용하여 구현할 수 있습니다. 보통 `Scaffold`의 `drawer` 속성에 추가하며, 햄버거 메뉴 버튼을 눌러 열 수 있습니다.  

---

## 1️⃣ **기본 사이드바 (Drawer) 구현**  
### ✅ **기본 코드 예제**
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false, // 디버그 배너 숨기기
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Flutter 사이드바 예제')),
      drawer: Drawer(
        child: ListView(
          padding: EdgeInsets.zero,
          children: [
            DrawerHeader(
              decoration: BoxDecoration(color: Colors.blue),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Icon(Icons.account_circle, size: 60, color: Colors.white),
                  SizedBox(height: 10),
                  Text(
                    '사용자 이름',
                    style: TextStyle(color: Colors.white, fontSize: 18),
                  ),
                  Text(
                    'user@email.com',
                    style: TextStyle(color: Colors.white70, fontSize: 14),
                  ),
                ],
              ),
            ),
            ListTile(
              leading: Icon(Icons.home),
              title: Text('홈'),
              onTap: () {
                Navigator.pop(context); // 사이드바 닫기
              },
            ),
            ListTile(
              leading: Icon(Icons.settings),
              title: Text('설정'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
            ListTile(
              leading: Icon(Icons.exit_to_app),
              title: Text('로그아웃'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
          ],
        ),
      ),
      body: Center(child: Text('메인 화면')),
    );
  }
}
```

### 🔹 **설명**
- `Scaffold`의 `drawer` 속성에 `Drawer` 위젯을 추가  
- `DrawerHeader`로 상단 사용자 정보 표시  
- `ListTile`을 사용하여 메뉴 항목 구성  
- `Navigator.pop(context)`를 호출하여 사이드바를 닫음  

---

## 2️⃣ **커스텀 스타일 적용하기**  
기본 스타일 외에도 `Container`, `BoxDecoration` 등을 사용하여 디자인을 변경할 수 있습니다.  

### 🎨 **커스텀 Drawer 예제**
```dart
drawer: Drawer(
  child: Container(
    color: Colors.grey[200], // 배경색 변경
    child: ListView(
      padding: EdgeInsets.zero,
      children: [
        DrawerHeader(
          decoration: BoxDecoration(color: Colors.deepPurple),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              CircleAvatar(
                radius: 30,
                backgroundImage: NetworkImage('https://example.com/user.jpg'),
              ),
              SizedBox(height: 10),
              Text(
                '사용자 이름',
                style: TextStyle(color: Colors.white, fontSize: 18),
              ),
              Text(
                'user@email.com',
                style: TextStyle(color: Colors.white70, fontSize: 14),
              ),
            ],
          ),
        ),
        ListTile(
          leading: Icon(Icons.dashboard, color: Colors.deepPurple),
          title: Text('대시보드'),
          onTap: () => Navigator.pop(context),
        ),
        ListTile(
          leading: Icon(Icons.person, color: Colors.deepPurple),
          title: Text('프로필'),
          onTap: () => Navigator.pop(context),
        ),
      ],
    ),
  ),
),
```

### ✨ **변경 사항**
- 배경 색상을 **연한 회색(Colors.grey[200])**으로 변경  
- `CircleAvatar`를 사용하여 사용자 프로필 사진 추가  
- 아이콘 및 텍스트 색상을 통일하여 깔끔한 UI 유지  

---

## 3️⃣ **오른쪽에서 열리는 Drawer**
기본적으로 `drawer`는 **왼쪽에서 열리지만**, `endDrawer` 속성을 사용하면 **오른쪽에서 열리는 Drawer**를 만들 수 있습니다.

### 📌 **오른쪽 사이드바 코드**
```dart
Scaffold(
  appBar: AppBar(title: Text('오른쪽 사이드바')),
  endDrawer: Drawer(
    child: ListView(
      children: [
        DrawerHeader(
          decoration: BoxDecoration(color: Colors.green),
          child: Text('오른쪽 메뉴', style: TextStyle(color: Colors.white, fontSize: 20)),
        ),
        ListTile(
          leading: Icon(Icons.info),
          title: Text('정보'),
          onTap: () => Navigator.pop(context),
        ),
      ],
    ),
  ),
  body: Center(child: Text('메인 화면')),
);
```
🔹 **`endDrawer`를 사용하면 오른쪽에서 열리는 사이드바를 구현할 수 있습니다.**  

---

## 4️⃣ **Drawer를 프로그래밍적으로 열고 닫기**
보통 **햄버거 아이콘(≡) 버튼**을 누르면 Drawer가 열리지만, `GlobalKey<ScaffoldState>`를 사용하여 버튼 클릭으로 직접 열 수도 있습니다.

### 🛠 **Drawer 열기/닫기 코드**
```dart
class HomeScreen extends StatelessWidget {
  final GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey<ScaffoldState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(
        title: Text('프로그램으로 Drawer 열기'),
        leading: IconButton(
          icon: Icon(Icons.menu),
          onPressed: () {
            _scaffoldKey.currentState?.openDrawer(); // Drawer 열기
          },
        ),
      ),
      drawer: Drawer(
        child: ListView(
          children: [
            DrawerHeader(
              decoration: BoxDecoration(color: Colors.blue),
              child: Text('사이드바', style: TextStyle(color: Colors.white)),
            ),
            ListTile(
              title: Text('홈'),
              onTap: () {
                _scaffoldKey.currentState?.openEndDrawer(); // 사이드바 닫기
              },
            ),
          ],
        ),
      ),
      body: Center(child: Text('메인 화면')),
    );
  }
}
```
🔹 **설명**
- `GlobalKey<ScaffoldState>`를 사용하여 `Scaffold`의 상태를 제어  
- `openDrawer()`를 호출하면 프로그램적으로 Drawer를 열 수 있음  

---

## 🚀 **정리**
| 기능 | 코드 |
|------|------|
| 기본 사이드바 | `Scaffold`의 `drawer` 속성 사용 |
| 오른쪽 사이드바 | `Scaffold`의 `endDrawer` 속성 사용 |
| Drawer 스타일 변경 | `DrawerHeader`, `Container`, `BoxDecoration` 활용 |
| Drawer 프로그래밍으로 제어 | `GlobalKey<ScaffoldState>` 사용 |

이제 **Flutter에서 사이드바(Drawer)를 자유롭게 활용할 수 있습니다!**  
추가 질문이 있으면 언제든지 물어보세요! 😊🚀
