ALTER TABLE work_items_clean
ADD iteration_path NVARCHAR(255),
    area_path NVARCHAR(255),
    reason NVARCHAR(255),
    changed_date NVARCHAR(255),
    priority INT;
