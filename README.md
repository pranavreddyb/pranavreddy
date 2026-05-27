data = response.json()

# STEP 2 — Extract fields

work_item_id = data["id"]

title = data["fields"].get("System.Title")

state = data["fields"].get("System.State")

work_item_type = data["fields"].get("System.WorkItemType")

assigned_to = data["fields"].get("System.AssignedTo", {}).get("displayName")

created_date = data["fields"].get("System.CreatedDate")


payload_json = json.dumps(data)
