created_by = fields.get("System.CreatedBy", {}).get("displayName")
changed_by = fields.get("System.ChangedBy", {}).get("displayName")
team_project = fields.get("System.TeamProject")
tags = fields.get("System.Tags")
