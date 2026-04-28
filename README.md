import streamlit as st
import pandas as pd
from services.mock_data import get_mock_data

st.set_page_config(page_title="Test Harness", layout="wide")

st.title("🧪 Test Harness")
st.caption("Search scenario validation")

# Load data
data = get_mock_data()
df = pd.DataFrame(data)

# -----------------------------------
# Test Cases
# -----------------------------------
tests = [
    {
        "Test ID": "BASIC-001",
        "Scenario": "Search Susan",
        "Expected": "1 result",
        "Actual": len(df[df["ClientName"].str.contains("Susan", case=False)]),
    },
    {
        "Test ID": "FILTER-001",
        "Scenario": "State = Florida",
        "Expected": "1 result",
        "Actual": len(df[df["State"] == "Florida"]),
    },
    {
        "Test ID": "FORM-001",
        "Scenario": "Form = W-2",
        "Expected": "1 result",
        "Actual": len(df[df["FormType"] == "W-2"]),
    },
    {
        "Test ID": "HIGHWAGE-001",
        "Scenario": "Wages > 100000",
        "Expected": "1 result",
        "Actual": len(df[df["Wages"] > 100000]),
    },
]

results = []

for test in tests:
    status = "PASS" if test["Actual"] >= 1 else "FAIL"
    results.append({
        "Test ID": test["Test ID"],
        "Scenario": test["Scenario"],
        "Expected": test["Expected"],
        "Actual": test["Actual"],
        "Status": status
    })

result_df = pd.DataFrame(results)

# -----------------------------------
# Output
# -----------------------------------
st.dataframe(result_df, use_container_width=True, hide_index=True)

pass_count = len(result_df[result_df["Status"] == "PASS"])
fail_count = len(result_df[result_df["Status"] == "FAIL"])

col1, col2 = st.columns(2)
col1.metric("Passed", pass_count)
col2.metric("Failed", fail_count)
