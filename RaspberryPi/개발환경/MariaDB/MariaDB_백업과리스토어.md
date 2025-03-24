MariaDB에서 파일 백업과 복원 방법에 대해 설명드리겠습니다. 데이터베이스를 백업하고 복원하는 과정은 데이터 손실을 방지하고 데이터베이스를 이전 상태로 복구할 때 매우 유용합니다.

### 1. MariaDB 데이터베이스 백업 (Dump 방식)
MariaDB에서 데이터베이스 백업을 수행하려면 `mysqldump` 명령어를 사용합니다.

#### (1) 전체 데이터베이스 백업
전체 MariaDB 데이터베이스를 백업하려면 다음 명령어를 사용합니다. 이 명령은 모든 데이터베이스를 포함한 SQL 덤프 파일을 생성합니다.

```bash
sudo mysqldump -u root -p --all-databases > all_databases_backup.sql
```

- `-u root`: 루트 사용자로 로그인
- `-p`: 비밀번호 입력
- `--all-databases`: 모든 데이터베이스 백업
- `> all_databases_backup.sql`: 백업 파일로 저장

#### (2) 특정 데이터베이스 백업
특정 데이터베이스만 백업하려면 데이터베이스 이름을 지정합니다. 예를 들어, `my_database`라는 데이터베이스를 백업하려면:

```bash
sudo mysqldump -u root -p my_database > my_database_backup.sql
```

#### (3) 특정 테이블 백업
특정 데이터베이스 내에서 한 개 이상의 테이블만 백업하려면 데이터베이스 이름과 테이블 이름을 지정합니다.

```bash
sudo mysqldump -u root -p my_database table1 table2 > my_database_tables_backup.sql
```

### 2. MariaDB 데이터베이스 복원 (Restore)
백업한 SQL 덤프 파일을 사용하여 MariaDB 데이터베이스를 복원할 수 있습니다.

#### (1) 전체 데이터베이스 복원
전체 데이터베이스를 복원하려면 다음 명령어를 사용합니다.

```bash
sudo mysql -u root -p < all_databases_backup.sql
```

#### (2) 특정 데이터베이스 복원
특정 데이터베이스를 복원하려면 복원할 데이터베이스를 먼저 생성한 후, 백업 파일을 복원해야 합니다.

1. 먼저 복원할 데이터베이스를 생성합니다.

```sql
CREATE DATABASE my_database;
```

2. 그런 다음 백업 파일을 복원합니다.

```bash
sudo mysql -u root -p my_database < my_database_backup.sql
```

#### (3) 특정 테이블 복원
특정 테이블을 복원하려면 데이터베이스를 먼저 선택한 후, 해당 테이블만 복원합니다.

```bash
sudo mysql -u root -p my_database < my_database_tables_backup.sql
```

### 3. MariaDB 데이터베이스 파일 시스템 백업
MariaDB는 데이터베이스 파일을 디스크에 저장하므로, `mysqldump` 외에도 MariaDB의 데이터 파일을 직접 백업할 수 있습니다. 그러나 이 방법은 일반적으로 `mysqldump`를 사용할 수 없는 경우에만 사용하며, MariaDB 서버가 중지된 상태에서 수행하는 것이 안전합니다.

1. MariaDB 서비스 중지:
```bash
sudo systemctl stop mariadb
```

2. MariaDB 데이터 디렉토리 백업:
MariaDB의 데이터 디렉토리는 일반적으로 `/var/lib/mysql/`에 있습니다. 이 디렉토리를 백업하려면:

```bash
sudo tar -czvf mariadb_backup.tar.gz /var/lib/mysql/
```

3. MariaDB 서비스 재시작:
백업이 완료되면 MariaDB 서비스를 다시 시작합니다.

```bash
sudo systemctl start mariadb
```

### 4. 백업/복원 시 주의사항
- **`mysqldump` 방식**은 서버가 실행 중이어도 백업할 수 있기 때문에 가장 일반적으로 사용됩니다.
- **파일 시스템 방식**은 서버를 중지해야 하며, 데이터가 일관되게 백업됩니다.
- 백업 파일을 복원할 때 데이터베이스가 기존에 존재하지 않으면 먼저 데이터베이스를 생성해야 합니다.
- 복원 후, 데이터베이스가 정상적으로 작동하는지 확인해야 합니다.

이와 같이 MariaDB에서 데이터베이스 백업과 복원 작업을 손쉽게 할 수 있습니다.
