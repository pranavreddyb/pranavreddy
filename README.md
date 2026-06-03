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

print(response.status_code)
print(response.text)
