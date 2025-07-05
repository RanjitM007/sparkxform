# sparkxform

**sparkxform** is a lightweight and reusable PySpark transformation utility library designed for scalable and modular data engineering pipelines. It contains a growing collection of transformation functions for Spark DataFrames including ID generation, string cleaning, date parsing, and more.

---

## 📦 Features

- 🔢 Dynamic ID generation from existing tables
- ✂️ String cleaning (trimming, lowercasing, etc.)
- 📅 Date column parsing and standardization
- 🔄 Easily extendable with your own transformations
- 💼 Production-friendly Python packaging

---

## 📚 Installation

Clone the repository and install locally:

```bash
git clone https://github.com/RanjitM007/sparkxform.git
cd sparkxform
pip install -e .
```

Or

```python
pip install sparkxform
```

### 🔢 assign_next_id

```python
from sparkxform import assign_next_id

df = assign_next_id(spark, df, table_name='existing_table', column_name='storage_id')
```
### 📌 Description

`assign_next_id()` assigns a **uniform incremental ID** to all rows in the given DataFrame by:

- Querying the max ID from an external table via Spark SQL.
- Incrementing it by one.
- Creating (or overwriting) a column with that next ID value.

---

### ✅ Advantages

- Simple and fast for batch inserts with uniform IDs.
- Useful for tracking ingestion batches.
- Easily integrates with Hive/Spark SQL tables.
- Eliminates race conditions in single-threaded batch ETL flows.

---

### ⚠️ Disadvantages

- All rows get the same ID, so it is not suitable for row-level uniqueness.
- Requires the external table (`table_name`) to exist and be readable.
- Not thread-safe or atomic in distributed writes — use with care in concurrent workloads.
- Cannot assign unique row IDs (e.g., for primary keys) — for that use `monotonically_increasing_id()` or UUIDs.

---

### 🧠 Best For

- Appending batch metadata.
- Managing incremental inserts.
- Logging ingestion batches with shared identifiers.

---

### 🔁 Related Functions (coming soon)

- `assign_partitioned_ids()`
- `assign_uuid_column()`
- `generate_sequential_ids_by_group()`

---

Let me know if you'd like me to help you implement the **row-level unique ID generator**, **partition-aware version**, or add automated tests for this function.


