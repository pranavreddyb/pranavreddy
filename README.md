SELECT work_items_id, COUNT(*) AS Cnt
FROM dbo.raw_work_items
GROUP BY work_items_id
HAVING COUNT(*) > 1;
