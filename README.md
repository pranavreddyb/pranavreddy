conn = pyodbc.connect(
    'DRIVER={SQL Server};'
    'SERVER=UI-6JXS7H4\\SQLEXPRESS;'
    'DATABASE=AzureDevOpsDB;'
    'Trusted_Connection=yes;'
)

cursor = conn.cursor()

cursor.execute("""
INSERT INTO work_items (work_item_id, title, state)
VALUES (?, ?, ?)
""",
data["id"],
data["fields"]["System.Title"],
data["fields"]["System.State"]
)

conn.commit()

print("Inserted into SQL Server successfully")

conn.close()
