cursor.execute("""
IF NOT EXISTS (
    SELECT 1
    FROM work_items_clean
    WHERE work_item_id = ?
)
BEGIN
    INSERT INTO work_items_clean
    (
        work_item_id,
        title,
        state,
        work_item_type,
        assigned_to,
        created_date,
        created_by,
        iteration_path,
        area_path,
        reason,
        changed_date,
        priority,
        changed_by,
        team_project,
        tags
    )
    VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
END
""",
item["id"],
item["id"],
title,
state,
work_item_type,
assigned_to,
created_date,
created_by,
iteration_path,
area_path,
reason,
changed_date,
priority,
changed_by,
team_project,
tags
)
