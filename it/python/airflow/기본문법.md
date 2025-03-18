Apache Airflow는 워크플로우를 작성하고 실행하는 오픈소스 플랫폼입니다. 기본적으로 Python을 사용하여 DAG(Directed Acyclic Graph)를 정의하고 실행합니다.  

---

## 1. **Airflow 기본 개념**
### DAG (Directed Acyclic Graph)
- 작업(Task)들의 흐름을 정의한 그래프
- **DAG** 안에 여러 개의 **Task**가 존재
- 각 Task 간 의존성을 정의하여 순서를 결정

### Task
- 실행할 개별 작업 단위
- Operator를 사용하여 정의

### Operator
- Task를 수행하는 방식(예: Python 함수 실행, Bash 명령어 실행, SQL 쿼리 실행 등)
- 대표적인 Operator
  - `PythonOperator` : Python 함수를 실행
  - `BashOperator` : Shell 명령어 실행
  - `DummyOperator` : 아무 작업도 하지 않음 (연결만)
  - `EmailOperator` : 이메일 전송
  - `PostgresOperator` : PostgreSQL 실행
  - `MySqlOperator` : MySQL 실행

---

## 2. **Airflow DAG 기본 코드 예제**
Airflow DAG을 작성하려면 **Python 코드**로 `.py` 파일을 작성하여 Airflow의 `dags` 폴더에 저장해야 합니다.

### DAG 기본 예제
```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from airflow.utils.dates import days_ago

# DAG 기본 설정
dag = DAG(
    dag_id="my_first_dag",  # DAG 이름
    description="My first Airflow DAG",  # 설명
    schedule_interval="@daily",  # 실행 주기 (매일 실행)
    start_date=days_ago(1),  # 시작 날짜 (과거 날짜로 설정하여 즉시 실행 가능)
    catchup=False,  # 과거 실행 안 함
)

# Task 정의
task_1 = BashOperator(
    task_id="print_hello",  # Task ID
    bash_command="echo 'Hello, Airflow!'",  # 실행할 명령어
    dag=dag,  # DAG 할당
)

task_2 = BashOperator(
    task_id="print_goodbye",
    bash_command="echo 'Goodbye, Airflow!'",
    dag=dag,
)

# Task 실행 순서 정의
task_1 >> task_2  # task_1 실행 후 task_2 실행
```

---

## 3. **Airflow 주요 문법**
### 1) **DAG 설정**
```python
dag = DAG(
    dag_id="my_dag",
    schedule_interval="0 12 * * *",  # 매일 12시에 실행
    start_date=days_ago(2),
    catchup=False,
)
```
- `schedule_interval`: 실행 주기 설정 (`"@daily"`, `"@hourly"`, `"@weekly"`, `"0 12 * * *"` 등 가능)
- `start_date`: DAG 시작 날짜
- `catchup`: False일 경우, 과거 실행 안 함

---

### 2) **Operator 사용**
#### **PythonOperator (Python 함수 실행)**
```python
from airflow.operators.python import PythonOperator

def my_python_function():
    print("This is a Python function.")

python_task = PythonOperator(
    task_id="run_python_function",
    python_callable=my_python_function,
    dag=dag,
)
```

#### **BashOperator (Shell 명령어 실행)**
```python
from airflow.operators.bash import BashOperator

bash_task = BashOperator(
    task_id="print_date",
    bash_command="date",
    dag=dag,
)
```

#### **DummyOperator (의존성 연결용)**
```python
from airflow.operators.empty import EmptyOperator

start = EmptyOperator(task_id="start", dag=dag)
end = EmptyOperator(task_id="end", dag=dag)

start >> end
```

---

### 3) **Task 간 의존성 설정**
```python
task_1 >> task_2  # task_1 실행 후 task_2 실행
task_1 << task_2  # task_2 실행 후 task_1 실행
task_1 >> [task_2, task_3]  # task_1 실행 후 task_2, task_3 동시 실행
```

---

## 4. **Airflow DAG 실행 방법**
1. **Airflow 웹 UI에서 실행**
   - `airflow webserver` 실행 후, 웹 UI에서 DAG 활성화 후 실행

2. **CLI에서 실행**
   ```sh
   airflow dags list  # DAG 목록 확인
   airflow dags trigger my_first_dag  # DAG 실행
   airflow tasks test my_first_dag print_hello 2024-03-18  # 특정 Task 테스트 실행
   ```

---

## 5. **Airflow 실행 방법**
### 1) **Airflow 환경 설정**
```sh
export AIRFLOW_HOME=~/airflow  # 기본 디렉터리 설정
```

### 2) **Airflow 초기화**
```sh
airflow db init  # 데이터베이스 초기화
```

### 3) **Airflow 실행**
```sh
airflow webserver  # 웹 서버 실행 (localhost:8080)
airflow scheduler  # 스케줄러 실행
```

---

### ✅ **정리**
- **DAG**: 작업(Task)의 흐름을 정의하는 그래프
- **Task**: 개별 실행 단위 (Operator 사용)
- **Operator**: 실행 방식 (PythonOperator, BashOperator 등)
- **의존성**: `>>`, `<<`로 Task 간 순서 지정
- **실행 방법**: Web UI 또는 CLI 사용

Airflow를 활용하면 ETL, 데이터 파이프라인 등을 자동화할 수 있습니다. 필요에 따라 다양한 Operator와 설정을 추가하여 확장할 수 있습니다. 🚀
