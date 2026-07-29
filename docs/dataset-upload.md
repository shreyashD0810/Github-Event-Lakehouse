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
