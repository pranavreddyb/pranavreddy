SELECT TOP 20
JSON_VALUE(payload, '$.fields."System.Tags"') AS Tags
FROM dbo.raw_work_items;
