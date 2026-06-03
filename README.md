SELECT
    COUNT(*) AS TotalRows,
    COUNT(priority) AS PriorityFilled,
    COUNT(changed_by) AS ChangedByFilled,
    COUNT(area_path) AS AreaPathFilled,
    COUNT(iteration_path) AS IterationPathFilled
FROM dbo.work_items_clean;
