## **Airflow에서 `catchup`이란?**  
Airflow에서 `catchup`은 **DAG 활성화 후, 과거의 미실행된 일정들을 자동으로 실행할지 여부를 결정하는 기능**입니다.  
기본적으로 `catchup=True`로 설정되어 있으며, DAG이 활성화될 때 **과거 실행 일정까지 모두 실행하려고 시도**합니다.

---

## **1. `catchup`의 동작 방식**
Airflow는 DAG 실행을 `start_date` 이후부터 **모든 예약된 실행 일정에 따라 수행**합니다.  
즉, DAG이 비활성화된 상태에서 과거의 실행 일정이 존재하면, DAG을 활성화할 때 누락된 일정까지 모두 실행합니다.

### ✅ **예제: `catchup=True` (기본값)**
다음 DAG을 2024년 3월 1일에 활성화한다고 가정해 보겠습니다.

```python
from airflow import DAG
from airflow.operators.dummy import DummyOperator
from datetime import datetime

dag = DAG(
    "catchup_example",
    schedule_interval="0 12 * * *",  # 매일 정오(12:00)에 실행
    start_date=datetime(2024, 2, 25),  # 시작 날짜: 2월 25일
    catchup=True,  # 기본값 (과거 일정 실행)
)

task = DummyOperator(task_id="dummy_task", dag=dag)
```

💡 **Airflow의 실행 스케줄**  
- DAG이 3월 1일에 활성화되었지만, `start_date=2024-02-25`이므로  
  → **2월 25일부터 2월 29일까지 실행되지 않은 DAG을 모두 실행**함.  
- 3월 1일이 되면 DAG은 정상적으로 3월 1일 12:00에 실행됨.

📌 **결과:** DAG이 활성화될 때, 2월 25일~29일까지의 **미실행된 일정이 먼저 실행**되고, 이후 정상적으로 작동함.

---

## **2. `catchup=False`의 동작 방식**
과거의 DAG 실행을 **무시하고 최신 실행 일정부터 실행**하도록 하려면 `catchup=False`로 설정하면 됩니다.

```python
dag = DAG(
    "catchup_disabled_example",
    schedule_interval="0 12 * * *",  # 매일 정오(12:00)에 실행
    start_date=datetime(2024, 2, 25),  # 시작 날짜: 2월 25일
    catchup=False,  # 과거 일정 실행하지 않음
)
```

💡 **Airflow의 실행 스케줄**  
- DAG을 3월 1일에 활성화했지만 `catchup=False`이므로  
  → **2월 25일~2월 29일까지의 과거 실행 일정은 무시됨.**  
- 3월 1일 12:00부터 DAG이 정상적으로 실행됨.

📌 **결과:** DAG이 활성화된 시점에서 가장 가까운 실행 일정(미래)부터 실행됨.

---

## **3. `catchup`이 필요한 경우 vs. 필요하지 않은 경우**

✅ **`catchup=True`가 필요한 경우 (기본값)**
- DAG이 중요한 데이터를 **과거부터 순서대로 처리해야 하는 경우**  
- 예를 들어, **배치 처리, 데이터 백필링(Backfilling) 작업** 등  
  → 과거 데이터를 하나씩 채워 넣어야 하므로, `catchup=True`가 필요함.  

✅ **`catchup=False`가 적합한 경우**
- DAG이 최신 데이터만 처리하면 되는 경우 (예: 실시간 모니터링)  
- **과거 데이터를 무시하고, 현재 또는 미래의 데이터만 처리하면 되는 경우**  
  → 과거 데이터를 처리할 필요가 없으므로 `catchup=False`를 설정.  

---

## **4. `catchup=False`와 `max_active_runs=1` 조합**
- `catchup=False`를 설정하면 과거 실행 일정은 무시되지만,  
  **여러 DAG 실행이 동시에 실행될 가능성이 있음**  
- **이를 방지하려면 `max_active_runs=1`을 추가**하여 한 번에 하나의 실행만 허용할 수 있음.

```python
dag = DAG(
    "catchup_and_max_active_runs",
    schedule_interval="0 12 * * *",
    start_date=datetime(2024, 2, 25),
    catchup=False,  # 과거 일정 실행하지 않음
    max_active_runs=1,  # 동시에 실행되는 DAG 개수를 1로 제한
)
```

---

## **5. 결론**
- `catchup=True` (기본값)  
  → 과거의 미실행된 DAG 실행 일정을 채움.  
- `catchup=False`  
  → 과거 실행 일정은 무시하고 최신 실행 일정부터 실행.  

🔹 **데이터 백필링이 필요한 경우** → `catchup=True`  
🔹 **과거 실행 일정이 필요 없는 경우** → `catchup=False`  
