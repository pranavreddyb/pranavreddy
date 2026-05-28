import requests
import json
import pyodbc
from requests.auth import HTTPBasicAuth

organization = "DeloitteTaxTechnology"
project = "Vega"

pat = "YOUR_PAT_TOKEN"

work_item_id = 73519

url = f"https://dev.azure.com/{organization}/{project}/_apis/wit/workitems/{work_item_id}?api-version=7.1-preview.3"

response = requests.get(
    url,
    auth=HTTPBasicAuth('', pat)
)

print("Status Code:", response.status_code)

data = response.json()

print("ID:", data["id"])
print("Title:", data["fields"]["System.Title"])
print("State:", data["fields"]["System.State"])

with open("workitem_payload.json", "w") as file:
    json.dump(data, file, indent=4)

print("Payload saved to workitem_payload.json")

# -------------------------
# SQL CONNECTION
# -------------------------

conn = pyodbc.connect(
    'DRIVER={SQL Server};'
    'SERVER=UI-6JXS7H4\\SQLEXPRESS;'
    'DATABASE=AzureDevOpsDB;'
    'Trusted_Connection=yes;'
)

cursor = conn.cursor()

payload_json = json.dumps(data)

cursor.execute("""
INSERT INTO raw_work_items (work_items_id, payload)
VALUES (?, ?)
""",
work_item_id,
payload_json
)

# -------------------------
# TRANSFORMATION
# -------------------------

fields = data["fields"]

title = fields.get("System.Title")
state = fields.get("System.State")
work_item_type = fields.get("System.WorkItemType")
assigned_to = fields.get("System.AssignedTo", {}).get("displayName")
created_date = fields.get("System.CreatedDate")
iteration_path = fields.get("System.IterationPath")
area_path = fields.get("System.AreaPath")
reason = fields.get("System.Reason")
changed_date = fields.get("System.ChangedDate")
priority = fields.get("Microsoft.VSTS.Common.Priority")

cursor.execute("""
INSERT INTO work_items_clean
(work_item_id, title, state, work_item_type,
assigned_to, created_date, iteration_path,
area_path, reason, changed_date, priority)
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
