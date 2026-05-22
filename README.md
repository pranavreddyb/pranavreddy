import requests
from requests.auth import HTTPBasicAuth

organization = "DeloitteTaxTechnology"
project = "Vega"
pat = "YOUR_PAT_TOKEN"

url = f"https://dev.azure.com/{organization}/{project}/_apis/wit/workitems/1?api-version=7.0"

response = requests.get(
    url,
    auth=HTTPBasicAuth('', pat)
)

print("Status:", response.status_code)
print(response.json())
