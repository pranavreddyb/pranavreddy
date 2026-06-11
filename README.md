cursor.execute("""
INSERT INTO dbo.WorkItem_Root
(WorkItemId, WorkItemType, SourceProject, Payload)
VALUES (?, ?, ?, ?)
""",
1,
"Test",
"Vega",
'{"test":"data"}'
)

conn.commit()

print("INSERT SUCCESS")

exit()
