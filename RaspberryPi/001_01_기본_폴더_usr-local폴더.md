### **📌 `/usr/local/` 폴더의 역할**  

`/usr/local/`은 **사용자가 직접 설치한 프로그램 및 패키지**를 저장하는 곳입니다.  
이는 운영 체제(OS)가 관리하는 기본 시스템 폴더(`/usr/bin`, `/bin` 등)와 구분됩니다.

---

## **1. `/usr/local/`의 주요 특징**
✅ **OS의 기본 패키지와 독립적** → 시스템 패키지를 덮어쓰지 않음  
✅ **수동 설치된 소프트웨어용** → `apt` 같은 패키지 관리자가 아닌 직접 다운로드한 프로그램 저장  
✅ **일반 사용자는 쓰기 권한이 없음** → `sudo`를 사용해야 파일을 추가/수정 가능  

---

## **2. `/usr/local/`의 폴더 구조**
`/usr/local/` 폴더에는 여러 서브디렉터리가 존재합니다.

| 폴더 | 설명 |
|------|------|
| **`/usr/local/bin/`** | 직접 설치한 실행 파일(명령어) 저장 |
| **`/usr/local/sbin/`** | 시스템 관리자용 실행 파일 저장 (`root` 전용) |
| **`/usr/local/lib/`** | 직접 설치한 라이브러리 저장 |
| **`/usr/local/include/`** | 헤더 파일 저장(C, C++ 개발 시 사용) |
| **`/usr/local/share/`** | 설정 파일, 문서, 아이콘 등 저장 |
| **`/usr/local/etc/`** | 추가 프로그램의 설정 파일 저장 |
| **`/usr/local/src/`** | 소스 코드 저장 |

---

## **3. `/usr/local/`을 사용하는 이유**
📌 `/usr/bin/`이나 `/bin/` 같은 시스템 폴더에 프로그램을 설치하면 **운영 체제 업데이트 시 덮어씌워질 위험**이 있습니다.  
✅ `/usr/local/`을 사용하면 OS 업데이트와 무관하게 프로그램을 안전하게 유지할 수 있습니다.

---

## **4. 사용 예시**
### **예제 1: `/usr/local/bin`에 실행 파일 추가**
1. 사용자 정의 실행 파일을 `/usr/local/bin/`에 복사  
   ```bash
   sudo cp myscript /usr/local/bin/
   sudo chmod +x /usr/local/bin/myscript
   ```
2. 이제 터미널에서 `myscript` 명령어로 실행 가능  

### **예제 2: Flutter를 `/usr/local/`에 설치**
```bash
sudo mv flutter /usr/local/
export PATH="$PATH:/usr/local/flutter/bin"
```

---

### **🚀 결론**
- `/usr/local/`은 **사용자가 직접 설치한 프로그램을 저장하는 폴더**  
- 시스템 기본 프로그램(`/usr/bin/`)과 분리하여 안전하게 관리 가능  
- `bin`, `lib`, `share`, `etc` 등의 하위 폴더를 포함  
- 수동 설치한 프로그램(예: Flutter, Go, Python 패키지 등)이 주로 사용  

✅ **라즈베리파이에서 직접 설치한 프로그램을 안전하게 관리하려면 `/usr/local/`을 사용하는 것이 좋습니다!** 🚀
