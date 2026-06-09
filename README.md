Azure DevOps Work Item Ingestion - Detailed KT Document

1. Business Requirement

The objective is to extract Work Item data from Azure DevOps and store it in SQL Server in a structured format.

The data will later be used for:

- Reporting
- Analytics
- APIs
- Downstream processing

The first phase is focused on building the ingestion layer.

---

2. Existing Challenge

Initially, work items were being fetched one by one.

Process:

Work Item ID 1 → API Call
Work Item ID 2 → API Call
Work Item ID 3 → API Call

...

For approximately 1490 work items:

- Around 1490 API calls were made
- Execution time was around 30 minutes

This approach was not scalable.

---

3. Solution Implemented

Step 1 - Fetch Work Item IDs

We use Azure DevOps WIQL API.

Purpose:

- Dynamically fetch all Work Item IDs
- Avoid hardcoded IDs
- Automatically pick up new work items

Response:

Work Item IDs list

Example:

75595
75656
75674
75719

---

Step 2 - Fetch Work Item Details

After receiving IDs, we call Azure DevOps Work Items REST API.

API Limitation:

Maximum supported IDs per request = 200

Therefore:

1490 Work Items

↓

8 API Calls

Instead of:

1490 API Calls

This reduced execution time from:

~30 minutes

to

~20 seconds

---

4. APIs Used

WIQL API

Purpose:
Fetch Work Item IDs.

Work Items REST API

Purpose:
Fetch complete work item payload.

Returns:

- ID
- Fields
- State
- Assigned User
- Dates
- Tags
- Priority
- Complete metadata

Response format is JSON.

---

5. Current Flow

Azure DevOps

↓

WIQL Query

↓

Work Item IDs

↓

Batch Processing (200 IDs per Request)

↓

Work Items REST API

↓

JSON Response

↓

SQL Server

---

6. Tables

work_items_clean

Purpose:

Store parsed fields in relational format.

Columns include:

- work_item_id
- title
- state
- work_item_type
- assigned_to
- created_date
- created_by
- changed_by
- changed_date
- area_path
- iteration_path
- priority
- tags
- team_project

Used for:

- Reporting
- Queries
- Dashboards

---

7. Performance Improvements

Before:

1490 API calls

Execution time:

~30 minutes

After:

8 API calls

Execution time:

~20 seconds

Improvement:

More than 95% reduction in execution time.

---

8. Data Quality Fixes Implemented

Duplicate Prevention

Added UNIQUE constraint on:

work_item_id

Purpose:

Prevent duplicate insertion.

---

Date Conversion

Azure DevOps returns dates in:

2026-04-10T18:46:12.073Z

Converted to:

2026-04-10 18:46:12.073

Before inserting into SQL.

---

9. Current Requirement

New requirement received from Sripriya.

Need to create:

WorkItem_Root

Structure:

- Index
- WorkItemId
- WorkItemType
- SourceProject
- Payload

Payload should contain:

Complete Azure DevOps JSON response.

Example:

{
"id": 75595,
"fields": {...},
"relations": [...],
"url": "..."
}

Purpose:

Store raw data before transformation.

---

10. Future Flow

Azure DevOps

↓

WorkItem_Root

(Raw Payload)

↓

work_items_clean

(Structured Data)

↓

Reporting / APIs

This ensures that any new fields can be extracted later without calling Azure DevOps again.

---

11. How To Run

Open terminal.

Execute:

python get_ids.py

Expected Output:

Batch 1: Retrieved 200 items

Batch 2: Retrieved 200 items

...

All work items inserted successfully

Total time taken: ~20 seconds

---

12. Validation

Check row count:

SELECT COUNT(*)
FROM work_items_clean;

Check sample records:

SELECT TOP 10 *
FROM work_items_clean;

Check duplicates:

SELECT work_item_id, COUNT()
FROM work_items_clean
GROUP BY work_item_id
HAVING COUNT() > 1;

---

13. Current Status

Completed:

- Dynamic Work Item retrieval
- Batch Processing
- SQL Loading
- Date Conversion
- Duplicate Prevention
- Data Validation

Pending:

- WorkItem_Root creation
- Raw payload storage
- Future transformations
