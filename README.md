import streamlit as st
import pandas as pd
from services.mock_data import get_mock_data

def show_test_harness():
    st.title("🧪 Test Harness")
    st.caption("Search scenario validation")

    df = pd.DataFrame(get_mock_data())

    tests = []

    tests.append({
        "Test ID": "BASIC-001",
        "Scenario": "Search Susan",
        "Expected": "1 result",
        "Actual": len(df[df["ClientName"].str.contains("Susan", case=False)]),
    })

    tests.append({
        "Test ID": "FILTER-001",
        "Scenario": "State = Florida",
        "Expected": "1 result",
        "Actual": len(df[df["State"] == "Florida"]),
    })

    tests.append({
        "Test ID": "FLAG-001",
        "Scenario": "Missing Employer",
        "Expected": "1 result",
        "Actual": len(df[df["EmployerName"] == ""]),
    })

    result_df = pd.DataFrame(tests)

    result_df["Status"] = result_df.apply(
        lambda row: "PASS" if str(row["Actual"]).startswith("1") else "CHECK",
        axis=1
    )

    st.dataframe(result_df, use_container_width=True)
