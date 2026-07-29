# Uploading GitHub Archive Data to Databricks

This guide explains how to upload a GitHub Archive dataset to a Databricks Volume and load it into a PySpark DataFrame for further processing.

## Prerequisites

- Databricks Workspace
- Unity Catalog enabled
- A Catalog and Schema created (e.g., `workspace.github_event_lakehouse`)
- GitHub Archive dataset downloaded locally

---

## Step 1: Create a Volume

Create a Unity Catalog Volume to store the raw GitHub Archive files.

```sql
CREATE VOLUME IF NOT EXISTS workspace.github_event_lakehouse.raw_data;
```

---

## Step 2: Download the Dataset

Download the required hourly GitHub Archive file from the GitHub Archive website.

Example file:

```
2025-01-15-12.json.gz
```

---

## Step 3: Upload the Dataset

1. Open your Databricks Workspace.
2. Navigate to:

```
Catalog
└── workspace
    └── github_event_lakehouse
        └── Volumes
            └── raw_data
```

3. Click **Upload**.
4. Select the downloaded file (`2025-01-15-12.json.gz`).
5. Wait for the upload to finish.

The uploaded file will be available at:

```text
/Volumes/workspace/github_event_lakehouse/raw_data/2025-01-15-12.json.gz
```

---

## Step 4: Verify the Upload

Run the following command to verify that the file exists in the Volume.

```python
display(dbutils.fs.ls("/Volumes/workspace/github_event_lakehouse/raw_data"))
```

Expected output:

```
2025-01-15-12.json.gz
```

---

## Step 5: Load the Dataset

Read the compressed JSON file directly into a PySpark DataFrame.

```python
df = spark.read.json(
    "/Volumes/workspace/github_event_lakehouse/raw_data/2025-01-15-12.json.gz"
)
```

---

## Step 6: Validate the Data

Inspect the dataset before beginning data transformations.

```python
df.printSchema()

print(f"Rows: {df.count()}")
print(f"Columns: {len(df.columns)}")

df.show(5, truncate=False)
```

---

## Next Steps

After successfully loading the dataset, you can proceed with the Medallion Architecture:

- **Bronze Layer** – Store the raw GitHub events.
- **Silver Layer** – Flatten nested structures, clean data, and extract common fields.
- **Gold Layer** – Build analytical tables and dashboards for repository, contributor, and organization insights.
