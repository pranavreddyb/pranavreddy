import requests
from requests.auth import HTTPBasicAuth

organization = "DeloitteTaxTechnology"
project = "Vega"
pat = "YOUR_PAT"

url = f"https://dev.azure.com/{organization}/{project}/_apis/wit/wiql?api-version=7.0"

query = {
    "query": """
    SELECT [System.Id]
    FROM WorkItems
    WHERE [System.TeamProject] = 'Vega'
    """
}

response = requests.post(
    url,
    json=query,
    auth=HTTPBasicAuth('', pat)
)

# ADD HERE ↓↓↓

data = response.json()

work_item_ids = [item["id"] for item in data["workItems"]]

print("Total Work Items:", len(work_item_ids))

for work_item_id in work_item_ids[:5]:

    workitem_url = (
        f"https://dev.azure.com/{organization}/{project}"
        f"/_apis/wit/workitems/{work_item_id}?api-version=7.0"
    )

    response = requests.get(
        workitem_url,
        auth=HTTPBasicAuth('', pat)
    )

    if response.status_code != 200:
        print(f"Failed to fetch {work_item_id}")
        continue

    data = response.json()

    print(
        "ID:", data["id"],
        "| Title:", data["fields"].get("System.Title"),
        "| State:", data["fields"].get("System.State")
    )
