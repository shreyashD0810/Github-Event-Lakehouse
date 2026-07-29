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
