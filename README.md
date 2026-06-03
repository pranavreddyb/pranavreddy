SELECT TOP 1
    work_items_id,
    JSON_VALUE(payload, '$.fields."System.AreaPath"') AS AreaPath,
    JSON_VALUE(payload, '$.fields."System.IterationPath"') AS IterationPath,
    JSON_VALUE(payload, '$.fields."System.Reason"') AS Reason,
    JSON_VALUE(payload, '$.fields."System.CreatedDate"') AS CreatedDate,
    JSON_VALUE(payload, '$.fields."System.ChangedDate"') AS ChangedDate,
    JSON_VALUE(payload, '$.fields."System.TeamProject"') AS TeamProject
FROM dbo.raw_work_items;
