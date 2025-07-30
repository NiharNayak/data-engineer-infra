## 🧪 Take-Home Task: Real-Time Ingestion with Delivery Guarantees & Data Correction

### **Context:**

You’re designing a real-time ingestion pipeline to process user activity events from a simulated source. This pipeline must support **at-least-once delivery**, handle **late-arriving events**, and process **source-side deletions or invalidations**.

---

### **Assignment Objectives:**

#### 1. **Simulate a Data Stream**

Build a producer that emits JSON records every second:

```json
{
  "event_id": "uuid",
  "user_id": "user123",
  "event_type": "click",
  "event_time": "2025-07-30T12:00:00Z",
  "received_time": "2025-07-30T12:00:03Z",
  "is_valid": true
}
```

##### Add the following behaviors:

* Randomly **delay \~10%** of messages by 30–60 seconds.
* For **5–10% of previously sent events**, emit a **"correction event"** after a short delay:

  * **Either mark them as `is_valid: false`** to simulate logical deletion.
  * Or emit a special **tombstone message** (if using Kafka-like systems) with just the `event_id`.

---

#### 2. **Ingestion Pipeline**

* Ingest the stream and write data into your target store (e.g., warehouse, lake, or DB).
* Handle late-arriving data and ensure **correct event-time placement**.
* Handle **updates/deletes** based on:

  * A flag (`is_valid: false`)
  * Or a tombstone event (depending on the ingestion tool).

---

#### 3. **Guarantees & Data Validation**

You must:

* Ensure **at-least-once delivery**: no event loss, allow duplicates (with deduplication plan).
* Ensure **late event correctness**: events land in the correct time partition.
* **Handle deletions/invalidation**:

  * Mark or remove invalidated events from the target.
  * Avoid reprocessing deleted data incorrectly.

##### Include a validation step/script to:

* Ensure no record is missing.
* Ensure all corrections/deletes are reflected in the target.
* Verify deduplication strategy or explain handling of duplicates.

---

#### 4. **Bonus (Optional):**

* Add **integration tests** for:

  * Ingestion
  * Late data
  * Deleted/invalidated events
* Include a **brief observability/logging** approach: show metrics for late events, deletions, duplicates, ingestion lag.

---

### **Deliverables:**

1. Source code.
2. `README.md` with:

   * Setup + run instructions.
   * Design summary (tools, approach).
   * Handling strategy for late data, duplicates, deletions.
   * Scaling considerations for production.

---

### **Expected Time Commitment:** 4–6 hours (including optional parts)
