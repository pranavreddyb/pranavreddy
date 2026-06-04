for i in range(0, len(work_item_ids), 200):

    batch_ids = work_item_ids[i:i+200]

    ids_string = ",".join(str(x) for x in batch_ids)

    batch_url = (
        f"https://dev.azure.com/{organization}/{project}"
        f"/_apis/wit/workitems?ids={ids_string}&api-version=7.0"
    )

    response = requests.get(
        batch_url,
        auth=HTTPBasicAuth('', pat)
    )

    data = response.json()

    print(
        f"Batch {i//200 + 1}: Retrieved",
        len(data["value"]),
        "items"
    )

    for item in data["value"]:
        # existing insert logic here
