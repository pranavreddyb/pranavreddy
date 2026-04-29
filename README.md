import streamlit as st
import pandas as pd
from services.mock_data import get_mock_data

def show_dashboard():
    st.title("📊 Tax Search Dashboard")
    st.caption("Smart search for tax filing records")

    df = pd.DataFrame(get_mock_data())

    query = st.text_input(
        "Search by client, employer, state, or phrase"
    )

    col1, col2, col3, col4 = st.columns(4)

    with col1:
        year = st.selectbox(
            "Year",
            ["All"] + sorted(df["TaxYear"].astype(str).unique().tolist())
        )

    with col2:
        form = st.selectbox(
            "Form",
            ["All"] + sorted(df["FormType"].unique().tolist())
        )

    with col3:
        state = st.selectbox(
            "State",
            ["All"] + sorted(df["State"].unique().tolist())
        )

    with col4:
        flag = st.selectbox(
            "Flags",
            ["All", "High Wage", "Missing SSN", "Missing Employer"]
        )

    filtered = df.copy()

    if query:
        q = query.lower()
        filtered = filtered[
            filtered.astype(str)
            .apply(lambda row: row.str.lower().str.contains(q).any(), axis=1)
        ]

    if year != "All":
        filtered = filtered[filtered["TaxYear"].astype(str) == year]

    if form != "All":
        filtered = filtered[filtered["FormType"] == form]

    if state != "All":
        filtered = filtered[filtered["State"] == state]

    if flag == "High Wage":
        filtered = filtered[filtered["Wages"] > 90000]

    elif flag == "Missing SSN":
        filtered = filtered[
            (filtered["SSN"] == "") |
            (filtered["SSN"] == "N/A")
        ]

    elif flag == "Missing Employer":
        filtered = filtered[
            (filtered["EmployerName"] == "") |
            (filtered["EmployerName"] == "N/A")
        ]

    m1, m2, m3, m4 = st.columns(4)

    m1.metric("Total Records", len(filtered))
    m2.metric("High Wage", len(filtered[filtered["Wages"] > 90000]))
    m3.metric(
        "Missing SSN",
        len(filtered[
            (filtered["SSN"] == "") |
            (filtered["SSN"] == "N/A")
        ])
    )
    m4.metric("States Covered", filtered["State"].nunique())

    st.subheader(f"Results: {len(filtered)}")

    csv = filtered.to_csv(index=False).encode("utf-8")

    st.download_button(
        "📥 Download Results CSV",
        data=csv,
        file_name="results.csv",
        mime="text/csv"
    )

    st.dataframe(filtered, use_container_width=True)
