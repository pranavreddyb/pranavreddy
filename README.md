
ids = work_item_ids[:5]

ids_string = ",".join(str(i) for i in ids)

url = (
    f"https://dev.azure.com/{organization}/{project}"
    f"/_apis/wit/workitems?ids={ids_string}&api-version=7.0"
)

response = requests.get(
    url,
    auth=HTTPBasicAuth('', pat)
)

data = response.json()

print("Returned Work Items:", len(data["value"]))
