# TRANSFORMATION

work_item_id = data["id"]

title = data["fields"].get("System.Title")

state = data["fields"].get("System.State")

work_item_type = data["fields"].get("System.WorkItemType")

assigned_to = data["fields"].get("System.AssignedTo", {}).get("displayName")

created_date = data["fields"].get("System.CreatedDate")

iteration_path = data["fields"].get("System.IterationPath")

area_path = data["fields"].get("System.AreaPath")

reason = data["fields"].get("System.Reason")

changed_date = data["fields"].get("System.ChangedDate")

priority = data["fields"].get("Microsoft.VSTS.Common.Priority")


# SQL CONNECTION

conn = pyodbc.connect(
    'DRIVER={SQL Server};'
    'SERVER=UI-6JXS7H4\\SQLEXPRESS;'
    'DATABASE=AzureDevopsDB;'
    'Trusted_Connection=yes;'
)

cursor = conn.cursor()


# INSERT CLEAN DATA

cursor.execute("""
INSERT INTO work_items_clean
(
    work_item_id,
    title,
    state,
    work_item_type,
    assigned_to,
    created_date,
    iteration_path,
    area_path,
    reason,
    changed_date,
    priority
)

VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
""",

work_item_id,
title,
state,
work_item_type,
assigned_to,
created_date,
iteration_path,
area_path,
reason,
changed_date,
priority

)

conn.commit()

print("Clean transformed data inserted successfully")

conn.close()
