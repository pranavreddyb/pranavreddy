cursor.execute("""
INSERT INTO work_items_clean
(work_item_id, title, state, work_item_type, assigned_to, created_date)
VALUES (?, ?, ?, ?, ?, ?)
""",
work_item_id,
title,
state,
work_item_type,
assigned_to,
created_date
)
