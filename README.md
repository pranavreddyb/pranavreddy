UPDATE w
SET
    w.area_path = JSON_VALUE(r.payload, '$.fields."System.AreaPath"'),
    w.iteration_path = JSON_VALUE(r.payload, '$.fields."System.IterationPath"'),
    w.reason = JSON_VALUE(r.payload, '$.fields."System.Reason"'),
    w.created_date = JSON_VALUE(r.payload, '$.fields."System.CreatedDate"'),
    w.changed_date = JSON_VALUE(r.payload, '$.fields."System.ChangedDate"'),
    w.team_project = JSON_VALUE(r.payload, '$.fields."System.TeamProject"')
FROM dbo.work_items_clean w
INNER JOIN dbo.raw_work_items r
    ON w.work_item_id = r.work_items_id;
