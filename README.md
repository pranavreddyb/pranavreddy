SELECT TOP 1
    JSON_VALUE(payload, '$.fields."Microsoft.VSTS.Common.Priority"') AS Priority,
    JSON_VALUE(payload, '$.fields."System.ChangedBy".displayName') AS ChangedBy,
    JSON_VALUE(payload, '$.fields."System.Tags"') AS Tags
FROM dbo.raw_work_items;
