created_date = fields.get("System.CreatedDate")
iteration_path = fields.get("System.IterationPath")
area_path = fields.get("System.AreaPath")
reason = fields.get("System.Reason")
changed_date = fields.get("System.ChangedDate")

priority = fields.get("Microsoft.VSTS.Common.Priority")

changed_by = fields.get(
    "System.ChangedBy", {}
).get("displayName")

team_project = fields.get("System.TeamProject")

tags = fields.get("System.Tags")
