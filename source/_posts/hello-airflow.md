---
title: hello-airflow
date: 2025-04-26
tags: [Airflow, 資料工程, 排程管理]
categories: [學習筆記]
---

## Airflow vs Laravel 排程

最近查了一些資料，發現資料工程上常使用 Airflow 來管理排程。之前使用 Laravel 開發時，Laravel 也有 Scheduler 可以管理排程，因此我好奇 Airflow 到底厲害在哪裡。

經過研究後，我整理出以下兩點結論@@：

1. **流程相依性**

   - Airflow 的排程具有相依性，因為他本身就內建有流程相依的語法

   - Laravel 的排程則比較獨立，若要實現相依性需要額外撰寫大量程式碼，且會增加彼此間的耦合度，進而提高測試與維護難度。

2. **排程管理與維護**

   - 當排程數量眾多時，Laravel 由於缺乏階層與流程結構，除非所有排程都是由同一人開發，否則接手者需要透過觸發週期或時間點推敲整體資料流程與業務流程。
  
   - 而且還會需要依賴外部文件來對照理解，增加維護的複雜度。

感覺起來airflow很厲害哈哈，因為之前在公司畫流程圖時候，也覺得滿好玩的，那既然Airflow主打一個流程很強的優點，所以我想說來架看看好了＠＠

## 本地啟動指令

使用 Docker Compose 最快，指令＋說明如下：

- `curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.8.1/docker-compose.yaml'`  
  下載官方範例的 `docker-compose.yaml` 檔案。

- `docker-compose up airflow-init`  
  初始化資料庫及相關設定。

- `docker-compose up`  
  啟動整個 Airflow 系統，包括 Web UI、Scheduler 等服務。

啟動完成後，打開瀏覽器並訪問 [http://localhost:8080](http://localhost:8080) 即可看到 Airflow 的介面，功能豐富且專業。

預設帳號密碼皆為 `airflow`。

## DAG 實作範例

接著準備一個簡單的 Python 檔案（Airflow 專有名詞稱為 DAG），命名為 `hello_airflow.py`，並放置在 `dags` 資料夾中：

```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

def say_hello():
    print("Hello, Airflow!")

with DAG(
    dag_id="hello_airflow",
    start_date=datetime(2025, 4, 25),
    schedule_interval=None,  # 手動觸發
    catchup=False,
) as dag:
    hello_task = PythonOperator(
        task_id="say_hello_task",
        python_callable=say_hello,
    )
```

這個 DAG 非常簡單，執行時會在 log 中印出一行 "Hello, Airflow!"。

## 介面操作步驟

打開 Airflow Web UI（預設為 8080 端口）後，可以依照以下步驟操作：

- **查看 DAG 清單**  
  頁面會顯示多個範例 DAG，我計畫之後修改 `docker-compose.yaml` 設定，移除這些範例，因為現今 AI 工具相當方便，直接查詢即可，不太需要大量範例。

- **觸發 DAG**  
  找到 `hello_airflow` 這個 DAG，點擊最右側的 **Trigger** 按鈕，即可手動觸發該 Python 檔案所定義的任務。

- **啟用排程**  
  若要讓 DAG 根據排程自動執行，點擊最左側的 **Toggle** 按鈕打開即可。

---

# 結語

未來可能會嘗試根據現有需求或業務邏輯，將 Airflow 組合成更完整的工作流程，感覺很好玩哈哈
