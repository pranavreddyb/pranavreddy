SELECT
    COUNT(*) AS TotalRows,
    COUNT(area_path) AS AreaPath,
    COUNT(iteration_path) AS IterationPath,
    COUNT(priority) AS Priority,
    COUNT(created_by) AS CreatedBy,
    COUNT(changed_by) AS ChangedBy,
    COUNT(team_project) AS TeamProject
FROM dbo.work_items_clean;
