라즈베리파이에서 **Visual Studio Code(VS Code)** 를 설정하는 방법을 안내해 드리겠습니다.  

---

## **1. VS Code 설치**  
라즈베리파이는 **ARM 아키텍처**이므로, 공식 **VS Code ARM 버전**을 설치해야 합니다.  

### **1-1. 패키지 목록 업데이트**  
```bash
sudo apt update && sudo apt upgrade -y
```

### **1-2. VS Code 설치**  
```bash
sudo apt install -y code
```

💡 만약 위 명령어로 설치되지 않는다면, 아래 방법을 사용하세요.  

### **수동 설치 (공식 .deb 패키지 다운로드)**  
```bash
wget -O code.deb https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-arm64
sudo dpkg -i code.deb
sudo apt --fix-broken install -y
```

설치 후 VS Code를 실행합니다.  
```bash
code
```

---

## **2. 필수 확장팩 설치**  
VS Code를 효율적으로 사용하기 위해 필요한 확장 기능을 설치합니다.  

### **터미널에서 설치 가능**
```bash
code --install-extension ms-python.python  # Python 지원
code --install-extension ms-vscode-remote.remote-ssh  # SSH 원격 개발
code --install-extension ms-vscode.cpptools  # C/C++ 개발
code --install-extension ms-vscode.node-debug2  # Node.js 디버깅
code --install-extension esbenp.prettier-vscode  # Prettier (코드 포맷팅)
```

또는 **VS Code → Extensions (Ctrl + Shift + X) → 필요한 확장 검색 및 설치**  

---

## **3. 기본 설정 변경 (최적화)**  
라즈베리파이는 성능이 낮기 때문에, 원활한 사용을 위해 최적화 설정을 적용합니다.  

### **설정 파일 열기**  
```bash
nano ~/.config/Code/User/settings.json
```

### **설정 추가**
```json
{
    "editor.fontSize": 14,
    "editor.smoothScrolling": false,
    "editor.cursorBlinking": "solid",
    "workbench.startupEditor": "none",
    "terminal.integrated.rendererType": "dom",
    "window.zoomLevel": 1
}
```
💡 **설정 내용**  
- `smoothScrolling: false` → 부드러운 스크롤 비활성화 (성능 향상)  
- `cursorBlinking: "solid"` → 커서 깜빡임 최소화 (CPU 부담 줄이기)  
- `startupEditor: "none"` → 시작 시 웰컴 페이지 비활성화  
- `rendererType: "dom"` → 터미널 속도 개선  

설정 적용 후 저장(`Ctrl + X` → `Y` → `Enter`).

---

## **4. VS Code 원격 접속 (SSH 연결)**
라즈베리파이에 원격으로 연결하여 VS Code에서 개발할 수도 있습니다.  

1️⃣ **라즈베리파이에서 SSH 활성화**  
```bash
sudo raspi-config
```
- **Interface Options → SSH → Enable** 선택  

2️⃣ **VS Code에서 SSH 확장 설치**
- **확장 마켓플레이스 (`Ctrl + Shift + X`)** → `Remote - SSH` 검색 후 설치  

3️⃣ **SSH 연결**  
VS Code에서 **Ctrl + Shift + P** → `Remote-SSH: Connect to Host` →  
```bash
ssh pi@라즈베리파이_아이피주소
```
비밀번호 입력 후 연결 완료 🎉  

---

## **5. 실행 & 테스트**  
VS Code를 실행하려면 터미널에서 입력하세요.  
```bash
code
```
이제 라즈베리파이에서 VS Code를 사용할 수 있습니다! 🚀
