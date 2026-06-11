cursor = conn.cursor()

print("\n===== CONNECTION CHECK =====")

cursor.execute("SELECT @@SERVERNAME")
print("SERVER:", cursor.fetchone()[0])

cursor.execute("SELECT DB_NAME()")
print("DATABASE:", cursor.fetchone()[0])

cursor.execute("""
SELECT TABLE_SCHEMA, TABLE_NAME
FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_NAME = 'WorkItem_Root'
""")

print("TABLES FOUND:", cursor.fetchall())

print("===== END CHECK =====\n")
