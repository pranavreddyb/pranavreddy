print("SERVER:", cursor.execute("SELECT @@SERVERNAME").fetchone()[0])
print("DATABASE:", cursor.execute("SELECT DB_NAME()").fetchone()[0])
