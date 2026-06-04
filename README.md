print("Total Work Items:", len(work_item_ids))

ids = work_item_ids[:5]

ids_string = ",".join(str(i) for i in ids)

batch_url = (
    f"https://dev.azure.com/{organization}/{project}"
    f"/_apis/wit/workitems?ids={ids_string}&api-version=7.0"
)

response = requests.get(
    batch_url,
    auth=HTTPBasicAuth('', pat)
)

data = response.json()

print("Returned:", len(data["value"]))
