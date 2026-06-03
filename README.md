UPDATE w
SET
    w.priority =
        JSON_VALUE(r.payload, '$.fields."Microsoft.VSTS.Common.Priority"'),

    w.changed_by =
        JSON_VALUE(r.payload, '$.fields."System.ChangedBy".displayName')

FROM dbo.work_items_clean w
INNER JOIN dbo.raw_work_items r
    ON w.work_item_id = r.work_items_id;
