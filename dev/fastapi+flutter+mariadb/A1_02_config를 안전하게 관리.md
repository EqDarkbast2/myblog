좋은 질문이에요! `app/core/config.py` 같은 설정 파일에는 **민감한 정보**(예: `SECRET_KEY`, DB 비밀번호 등)가 들어가기 때문에 **안전하게 관리**하는 것이 매우 중요합니다. 보안뿐 아니라 협업, 배포 자동화 시에도 중요한 부분이에요.

---

## ✅ 안전하게 관리하는 방법 요약

### 🔐 1. 민감한 정보는 `.env` 파일에 저장

예: `.env` 파일

```
SECRET_KEY=super-secret-key
DATABASE_URL=mysql+pymysql://user:pass@localhost:3306/yourdb
ACCESS_TOKEN_EXPIRE_MINUTES=60
```

---

### 🧠 2. `python-dotenv`를 사용하여 `.env` 불러오기

```bash
pip install python-dotenv
```

#### `app/core/config.py` 수정:

```python
import os
from dotenv import load_dotenv

load_dotenv()  # .env 파일 로드

SECRET_KEY = os.getenv("SECRET_KEY")
DATABASE_URL = os.getenv("DATABASE_URL")
ACCESS_TOKEN_EXPIRE_MINUTES = int(os.getenv("ACCESS_TOKEN_EXPIRE_MINUTES", "60"))
ALGORITHM = "HS256"
```

이제 민감한 정보는 코드에 직접 노출되지 않고 `.env`로 관리됩니다.

---

### 🧼 3. `.env` 파일은 Git에 **절대 포함하지 않기**

`.gitignore`에 추가:
```
.env
```

---

### 🔐 4. `.env.example` 파일로 템플릿 공유

```env
# .env.example
SECRET_KEY=your-secret-key
DATABASE_URL=mysql+pymysql://user:password@localhost:3306/yourdb
ACCESS_TOKEN_EXPIRE_MINUTES=60
```

- 실제 키는 포함하지 않고 구조만 제공합니다.
- 팀원은 `.env` 파일을 복사해서 만들 수 있습니다:
  ```bash
  cp .env.example .env
  ```

---

### ☁️ 5. 배포 환경에서는 `.env` 대신 환경변수 사용

예: Linux 서버에서 `export` 또는 `.bashrc`, `.service` 설정 등에 저장

```bash
export SECRET_KEY=your-prod-key
```

FastAPI는 `os.getenv()`를 통해 시스템 환경변수도 자동 인식합니다.

---

## 💡 정리

| 방법            | 용도                                      |
|-----------------|-------------------------------------------|
| `.env` 파일     | 로컬 개발용 안전한 환경 설정             |
| `.env.example`  | 팀/오픈소스 공유용 템플릿                |
| `os.getenv()`   | FastAPI가 안전하게 설정값을 읽도록 함    |
| `.gitignore`    | 민감 정보 Git에 포함 안 되도록 차단       |

---

원하시면 `config.py`를 더 구조화해서 `.class` 형태로 바꾸는 고급 방식도 소개해드릴게요!  
또는 이 설정과 함께 **Docker 환경변수**로 연동하는 법도 알려드릴 수 있어요.  
진행할까요?
