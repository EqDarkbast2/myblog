## 📌 **Flutter 위젯 종류 정리**  

Flutter는 모든 UI 요소를 **위젯(Widget)**으로 구성합니다. 위젯은 크게 **레이아웃, 입력, 애니메이션, 네비게이션, 미디어** 등으로 분류할 수 있습니다.  

---

## 1️⃣ **기본 위젯 (Basic Widgets)**
### ✅ **1. 텍스트 및 버튼 위젯**
| 위젯 | 설명 |
|------|------|
| **Text** | 텍스트 표시 (`Text("Hello, Flutter")`) |
| **RichText** | 여러 스타일의 텍스트 조합 (`RichText(text: TextSpan(...))`) |
| **ElevatedButton** | 기본 버튼 (`ElevatedButton(onPressed: () {}, child: Text("클릭"))`) |
| **TextButton** | 텍스트 버튼 (`TextButton(onPressed: () {}, child: Text("클릭"))`) |
| **OutlinedButton** | 외곽선 버튼 (`OutlinedButton(onPressed: () {}, child: Text("클릭"))`) |
| **IconButton** | 아이콘 버튼 (`IconButton(icon: Icon(Icons.add), onPressed: () {})`) |

👉 **예제 코드**
```dart
ElevatedButton(
  onPressed: () {
    print("버튼 클릭됨!");
  },
  child: Text("클릭"),
)
```

---

## 2️⃣ **레이아웃 위젯 (Layout Widgets)**
### ✅ **2. 컨테이너 및 정렬 관련 위젯**
| 위젯 | 설명 |
|------|------|
| **Container** | 박스 형태 UI (`Container(width: 100, height: 100, color: Colors.blue)`) |
| **Padding** | 내부 여백 추가 (`Padding(padding: EdgeInsets.all(10), child: Text("패딩 적용"))`) |
| **Align** | 정렬 조정 (`Align(alignment: Alignment.center, child: Text("정렬"))`) |
| **Center** | 중앙 정렬 (`Center(child: Text("중앙 정렬"))`) |
| **SizedBox** | 크기 조절 (`SizedBox(height: 20)`) |

👉 **예제 코드**
```dart
Container(
  padding: EdgeInsets.all(10),
  decoration: BoxDecoration(color: Colors.blue, borderRadius: BorderRadius.circular(10)),
  child: Text("컨테이너 예제", style: TextStyle(color: Colors.white)),
)
```

---

### ✅ **3. 레이아웃 구조 (Row, Column, Stack)**
| 위젯 | 설명 |
|------|------|
| **Row** | 가로 방향 정렬 |
| **Column** | 세로 방향 정렬 |
| **Stack** | 겹쳐진 UI 구성 |
| **Expanded** | 남은 공간을 차지하는 위젯 |
| **Flexible** | 비율에 맞게 크기 조절 |

👉 **예제 코드**
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    Text("아이템 1"),
    SizedBox(width: 10),
    Text("아이템 2"),
  ],
)
```

---

## 3️⃣ **입력 위젯 (Input Widgets)**
### ✅ **4. 폼 및 입력 필드**
| 위젯 | 설명 |
|------|------|
| **TextField** | 텍스트 입력 (`TextField(controller: myController)`) |
| **TextFormField** | 폼 입력 필드 |
| **Checkbox** | 체크박스 |
| **Radio** | 라디오 버튼 |
| **Switch** | 스위치 버튼 |
| **Slider** | 슬라이더 |
| **DropdownButton** | 드롭다운 메뉴 |

👉 **예제 코드**
```dart
TextField(
  decoration: InputDecoration(labelText: "이름 입력"),
)
```

---

## 4️⃣ **네비게이션 및 리스트 위젯 (Navigation & List Widgets)**
### ✅ **5. 네비게이션 및 탭바**
| 위젯 | 설명 |
|------|------|
| **AppBar** | 상단 바 (`AppBar(title: Text("제목"))`) |
| **BottomNavigationBar** | 하단 탭 바 |
| **TabBar** | 탭 인터페이스 |
| **Drawer** | 사이드바 메뉴 |
| **Navigator** | 화면 이동 (`Navigator.push(...)`) |

👉 **예제 코드**
```dart
AppBar(
  title: Text("Flutter 앱"),
  actions: [IconButton(icon: Icon(Icons.settings), onPressed: () {})],
)
```

---

### ✅ **6. 리스트 및 스크롤 관련 위젯**
| 위젯 | 설명 |
|------|------|
| **ListView** | 스크롤 가능한 리스트 |
| **GridView** | 격자형 리스트 |
| **SingleChildScrollView** | 단일 위젯 스크롤 |
| **ReorderableListView** | 드래그 가능한 리스트 |

👉 **예제 코드**
```dart
ListView(
  children: [
    ListTile(title: Text("항목 1")),
    ListTile(title: Text("항목 2")),
  ],
)
```

---

## 5️⃣ **미디어 및 애니메이션 위젯**
### ✅ **7. 이미지 및 아이콘**
| 위젯 | 설명 |
|------|------|
| **Image** | 이미지 표시 (`Image.network("https://example.com/image.jpg")`) |
| **Icon** | 아이콘 (`Icon(Icons.star, color: Colors.yellow)`) |

👉 **예제 코드**
```dart
Image.network("https://example.com/image.jpg", width: 100, height: 100)
```

---

### ✅ **8. 애니메이션 관련 위젯**
| 위젯 | 설명 |
|------|------|
| **AnimatedContainer** | 애니메이션이 적용된 컨테이너 |
| **Hero** | 페이지 간 애니메이션 |
| **FadeTransition** | 페이드 효과 애니메이션 |

👉 **예제 코드**
```dart
AnimatedContainer(
  duration: Duration(seconds: 1),
  width: 100,
  height: 100,
  color: Colors.blue,
)
```

---

## 6️⃣ **고급 위젯 (Advanced Widgets)**
### ✅ **9. 상태 관리 및 다이얼로그**
| 위젯 | 설명 |
|------|------|
| **FutureBuilder** | 비동기 데이터 처리 |
| **StreamBuilder** | 실시간 데이터 처리 |
| **Dialog** | 팝업 다이얼로그 (`showDialog(...)`) |

👉 **예제 코드**
```dart
showDialog(
  context: context,
  builder: (context) => AlertDialog(
    title: Text("경고"),
    content: Text("이 작업을 진행하시겠습니까?"),
    actions: [
      TextButton(onPressed: () => Navigator.pop(context), child: Text("취소")),
      ElevatedButton(onPressed: () {}, child: Text("확인")),
    ],
  ),
)
```

---

## 🚀 **정리**
| 카테고리 | 주요 위젯 |
|------|------|
| **기본 UI** | `Text`, `Button`, `Icon` |
| **레이아웃** | `Container`, `Row`, `Column`, `Stack` |
| **입력** | `TextField`, `Checkbox`, `Switch` |
| **네비게이션** | `AppBar`, `Drawer`, `Navigator` |
| **리스트 및 스크롤** | `ListView`, `GridView`, `SingleChildScrollView` |
| **미디어 및 애니메이션** | `Image`, `Hero`, `AnimatedContainer` |

위젯에 대한 추가 질문이 있다면 언제든지 물어보세요! 😊🚀
