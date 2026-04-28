import streamlit as st
import pandas as pd
from services.mock_data import get_mock_data

def show_test_harness():
    st.title("🧪 Test Harness")
    st.caption("Search scenario validation")

    # Load Data
    data = get_mock_data()
    df = pd.DataFrame(data)

    # -------------------------
    # Test Cases
    # -------------------------
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
            "Test ID": "FLAG-001",
            "Scenario": "High Wage > 90000",
            "Expected": "2 results",
            "Actual": len(df[df["Wages"] > 90000]),
        },
        {
            "Test ID": "MISS-001",
            "Scenario": "Missing SSN",
            "Expected": "1 result",
            "Actual": len(
                df[
                    (df["SSN"] == "") |
                    (df["SSN"] == "N/A")
                ]
            ),
        },
    ]

    # -------------------------
    # Evaluate PASS / FAIL
    # -------------------------
    results = []

    for test in tests:
        expected_num = int(test["Expected"].split()[0])
        status = "PASS" if test["Actual"] == expected_num else "FAIL"

        results.append({
            "Test ID": test["Test ID"],
            "Scenario": test["Scenario"],
            "Expected": test["Expected"],
            "Actual": f'{test["Actual"]} result(s)',
            "Status": status
        })

    result_df = pd.DataFrame(results)

    # -------------------------
    # Metrics
    # -------------------------
    col1, col2, col3 = st.columns(3)

    col1.metric("Total Tests", len(result_df))
    col2.metric("Passed", len(result_df[result_df["Status"] == "PASS"]))
    col3.metric("Failed", len(result_df[result_df["Status"] == "FAIL"]))

    # -------------------------
    # Show Results
    # -------------------------
    st.subheader("Test Results")
    st.dataframe(result_df, use_container_width=True)

    # -------------------------
    # Status Messages
    # -------------------------
    for _, row in result_df.iterrows():
        if row["Status"] == "PASS":
            st.success(f'{row["Test ID"]} - {row["Scenario"]} passed')
        else:
            st.error(f'{row["Test ID"]} - {row["Scenario"]} failed')
