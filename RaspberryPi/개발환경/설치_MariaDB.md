라즈베리파이에서 MariaDB를 설치하는 방법을 안내드리겠습니다. MariaDB는 MySQL의 오픈소스 포크로, 라즈베리파이와 같은 리눅스 기반 시스템에 쉽게 설치할 수 있습니다.

### 1. MariaDB 설치
먼저, 라즈베리파이에서 MariaDB를 설치합니다.

```bash
sudo apt update
sudo apt install mariadb-server
```

이 명령어는 MariaDB 서버를 설치합니다. 설치가 완료되면, MariaDB 서비스가 자동으로 시작됩니다.

### 2. MariaDB 서비스 상태 확인
MariaDB가 정상적으로 실행되고 있는지 확인하려면 다음 명령어를 사용하여 상태를 확인합니다.

```bash
sudo systemctl status mariadb
```

MariaDB가 실행 중이라면 다음과 비슷한 메시지가 나타납니다:
```
Active: active (running) since ...
```

### 3. MariaDB 초기 설정
MariaDB 설치 후, 기본 보안 설정을 진행해야 합니다. `mysql_secure_installation` 명령어를 실행하여 루트 비밀번호 설정 및 보안 관련 옵션을 설정합니다.

```bash
sudo mysql_secure_installation
```

이 과정에서 다음과 같은 설정을 할 수 있습니다:
- 루트 비밀번호 설정
- 익명 사용자 삭제
- 원격 루트 로그인 비활성화
- 테스트 데이터베이스 삭제

### 4. MariaDB 접속
MariaDB에 접속하려면 다음 명령어를 사용합니다.

```bash
sudo mysql -u root -p
```

위 명령어를 입력하면 비밀번호를 묻는 메시지가 나타납니다. `mysql_secure_installation`에서 설정한 루트 비밀번호를 입력하면 MariaDB 셸에 접속됩니다.

### 5. MariaDB 사용
MariaDB 셸에서 SQL 명령을 입력하여 데이터베이스를 관리할 수 있습니다. 예를 들어, 새로운 데이터베이스를 생성하려면:

```sql
CREATE DATABASE my_database;
```

### 6. MariaDB 종료
MariaDB 셸을 종료하려면 `exit`을 입력합니다.

```sql
exit;
```

### 7. MariaDB 서비스 관리
MariaDB 서비스를 중지, 시작 또는 재시작하려면 다음 명령어를 사용합니다.

- MariaDB 서비스 시작:
  ```bash
  sudo systemctl start mariadb
  ```
  
- MariaDB 서비스 중지:
  ```bash
  sudo systemctl stop mariadb
  ```

- MariaDB 서비스 재시작:
  ```bash
  sudo systemctl restart mariadb
  ```

이로써, 라즈베리파이에 MariaDB를 성공적으로 설치하고 사용할 수 있습니다.
