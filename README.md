payload_json = json.dumps(data)

cursor.execute("""
INSERT INTO raw_work_items
(work_items_id, payload)
VALUES (?, ?)
""",
data["id"],
payload_json
)

fields = data["fields"]

title = fields.get("System.Title")
state = fields.get("System.State")
work_item_type = fields.get("System.WorkItemType")
assigned_to = fields.get("System.AssignedTo", {}).get("displayName")
created_by = fields.get("System.CreatedBy", {}).get("displayName")

cursor.execute("""
INSERT INTO work_items_clean
(work_item_id, title, state, work_item_type, assigned_to, created_by)
VALUES (?, ?, ?, ?, ?, ?)
""",
data["id"],
title,
state,
work_item_type,
assigned_to,
created_by
)

print("Inserted:", data["id"])
