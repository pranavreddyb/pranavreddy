SELECT TOP 1
JSON_VALUE(payload, '$.fields.System.AreaPath') AS AreaPath,
JSON_VALUE(payload, '$.fields.System.IterationPath') AS IterationPath,
JSON_VALUE(payload, '$.fields.System.Reason') AS Reason,
JSON_VALUE(payload, '$.fields.System.CreatedDate') AS CreatedDate,
JSON_VALUE(payload, '$.fields.System.ChangedDate') AS ChangedDate
FROM dbo.raw_work_items;
