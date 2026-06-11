cursor.execute("""
INSERT INTO dbo.WorkItem_Root
(
    WorkItemId,
    WorkItemType,
    SourceProject,
    Payload
)
VALUES (?, ?, ?, ?)
""",
item["id"],
item["fields"].get("System.WorkItemType"),
project,
payload_json
)
