
## 🧪 Take-Home Task: Real-Time Ingestion and Delivery Guarantee

### **Context:**

You are working on a streaming data pipeline for ingesting real-time events (e.g., user activity logs) from a simulated source to a data warehouse or lake. You must build a pipeline that ensures **no data loss**, handles **late-arriving events**, and provides **at least-once delivery guarantees**.

---

### **Assignment Objectives:**

#### 1. **Simulate a Data Stream**

* Create a producer that emits JSON records every second. Example schema:

  ```json
  {
    "event_id": "uuid",
    "user_id": "user123",
    "event_type": "click",
    "event_time": "2025-07-30T12:00:00Z",
    "received_time": "2025-07-30T12:00:03Z"
  }
  ```
* Add logic to randomly delay **10% of the messages** (e.g., deliver them 30–60 seconds late).

---

#### 2. **Ingestion Pipeline**

* Use any combination of tools you prefer (e.g., Kafka, Kinesis, Spark, Flink, Airbyte, custom Python/Go scripts).
* Ingest the simulated data and write it into a destination layer (e.g., Postgres, Redshift, BigQuery, S3, or a warehouse of your choice).

---

#### 3. **Guarantees & Validation**

Implement the following:

* **At least-once delivery**: No message should be dropped. Duplicates are acceptable but must be handled.
* **Late event handling**: Late-arriving events should be processed and stored **in the correct partition/window** based on `event_time`.
* **Data completeness validation**: At the end of a run, provide a script or test to validate:

  * No record is missing.
  * All event\_ids are unique (or if duplicates exist, explain why and how you’d deduplicate).
  * Total counts per minute match between producer and target.

---

#### 4. **Bonus (Optional):**

* Add simple **integration tests** for the pipeline, testing end-to-end ingestion, duplicates, and late arrivals.
* Add **basic observability** (e.g., logs or a dashboard showing lag, count per minute, duplicates detected).

---

### **Deliverables:**

1. Source code (hosted in GitHub/GitLab or as a zip).
2. A `README.md` with:

   * Setup and run instructions.
   * Architecture summary (diagram optional).
   * Tradeoffs and assumptions.
   * How you would scale this for production (tools, patterns).
3. \[Optional] Jupyter Notebook or python script with validation tests.

---

### **Time Expected:** \~4–6 hours (including bonus, optional)
