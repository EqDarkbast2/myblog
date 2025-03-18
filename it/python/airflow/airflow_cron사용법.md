### Apache Airflow에서 Cron 사용법과 예시

Airflow에서 **cron 표현식**은 **DAG의 실행 스케줄을 정의할 때 사용**됩니다. Airflow는 `schedule_interval`에서 cron 표현식을 지원하며, DAG이 실행될 빈도를 설정하는 데 활용됩니다.  

---

## 1. **Airflow에서 Cron 표현식 사용 방법**
DAG을 정의할 때 `schedule_interval`에 cron 표현식을 사용하면 됩니다. 예를 들어:

```python
from airflow import DAG
from airflow.operators.dummy import DummyOperator
from datetime import datetime

# DAG 정의
dag = DAG(
    "cron_example_dag",
    schedule_interval="0 9 * * 1-5",  # 월~금 오전 9시 실행
    start_date=datetime(2024, 1, 1),
    catchup=False,
)

# 간단한 작업 정의
task = DummyOperator(task_id="dummy_task", dag=dag)
```
위 코드에서 `schedule_interval="0 9 * * 1-5"`은 월요일부터 금요일까지 **매일 오전 9시**에 실행된다는 의미입니다.

---

## 2. **Cron 표현식 기본 구조**
```
┌───────── 분 (0 - 59)
│ ┌────────── 시간 (0 - 23)
│ │ ┌─────────── 일 (1 - 31)
│ │ │ ┌──────────── 월 (1 - 12)
│ │ │ │ ┌───────────── 요일 (0 - 6) (일요일=0, 월요일=1, ... 토요일=6)
│ │ │ │ │
* * * * *
```

- `*` : 모든 값 (예: `*`을 사용하면 "매번"을 의미)
- `,` : 여러 개 선택 (예: `1,15` → 1일과 15일)
- `-` : 범위 지정 (예: `1-5` → 1일부터 5일까지)
- `/` : 주기 지정 (예: `*/5` → 5 단위로 실행)

---

## 3. **Cron 표현식 예제**

### (1) 매일 자정(00:00)에 실행
```python
schedule_interval="0 0 * * *"
```
➡️ **매일 자정(00:00)에 실행**

### (2) 매주 월요일 오전 8시 실행
```python
schedule_interval="0 8 * * 1"
```
➡️ **매주 월요일 오전 8시 실행**

### (3) 매월 1일과 15일, 오전 6시 실행
```python
schedule_interval="0 6 1,15 * *"
```
➡️ **매월 1일과 15일 오전 6시에 실행**

### (4) 매시간마다 실행
```python
schedule_interval="0 * * * *"
```
➡️ **매시간 정각에 실행**

### (5) 매 10분마다 실행
```python
schedule_interval="*/10 * * * *"
```
➡️ **매 10분마다 실행 (예: 00:00, 00:10, 00:20, ...)**

### (6) 매주 화요일과 목요일 오후 2시 실행
```python
schedule_interval="0 14 * * 2,4"
```
➡️ **매주 화요일과 목요일 오후 2시에 실행**

### (7) 매일 오전 9시부터 오후 6시까지 매 30분마다 실행
```python
schedule_interval="*/30 9-18 * * *"
```
➡️ **오전 9시~오후 6시 사이에 매 30분마다 실행**

### (8) 주말(토,일)마다 정오(12:00) 실행
```python
schedule_interval="0 12 * * 6,0"
```
➡️ **토요일과 일요일 정오(12:00)에 실행**

---

## 4. **Airflow에서 Cron 표현식 확인하는 방법**
Airflow는 `airflow dags next-execution` 명령어를 통해 다음 실행 시간을 확인할 수 있습니다.

```sh
airflow dags next-execution cron_example_dag
```
또한, Airflow 웹 UI의 **DAG 상세 페이지**에서 `Next Run`을 확인할 수도 있습니다.

---

## 5. **주의할 점**
1. **UTC 기준**  
   Airflow의 `schedule_interval`은 기본적으로 UTC 기준입니다. 한국 시간(KST, UTC+9)에서 실행하고 싶다면 `start_date`를 UTC로 변환하거나 `default_timezone='Asia/Seoul'`을 설정해야 합니다.
   
   ```python
   from airflow.utils.dates import days_ago
   from airflow.tz import timezone
   
   dag = DAG(
       "korean_time_dag",
       schedule_interval="0 9 * * *",  # UTC 기준 오전 9시 (KST 18시)
       start_date=days_ago(1),
       default_args={'timezone': timezone('Asia/Seoul')},
   )
   ```

2. **catchup 설정**  
   `catchup=False`를 설정하지 않으면, DAG이 활성화될 때 과거 실행 일정까지 모두 실행될 수 있습니다.

3. **Airflow 2.0+에서 사용 가능한 `timedelta`**  
   Cron 표현식 외에도 `timedelta`를 사용하여 간격을 설정할 수도 있습니다.

   ```python
   from datetime import timedelta
   schedule_interval=timedelta(hours=6)  # 6시간마다 실행
   ```

---
