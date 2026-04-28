import streamlit as st
import pandas as pd
from services.mock_data import get_mock_data

def show_dashboard():
    df = pd.DataFrame(get_mock_data())

    st.title("📊 Tax Search Dashboard")
    st.caption("Smart search for tax filing records")

    query = st.text_input("Search")

    col1, col2, col3 = st.columns(3)

    year = col1.selectbox("Year", ["All"] + sorted(df["TaxYear"].astype(str).unique()))
    form = col2.selectbox("Form", ["All"] + sorted(df["FormType"].unique()))
    state = col3.selectbox("State", ["All"] + sorted(df["State"].unique()))

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

    st.subheader(f"Results: {len(filtered)}")
    st.dataframe(filtered, use_container_width=True)
