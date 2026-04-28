import streamlit as st

def render_metrics(df):
    total_records = len(df)
    high_wage = len(df[df["Wages"] > 100000])
    missing_ssn = len(df[df["SSN"] == "N/A"])
    states = df["State"].nunique()

    col1, col2, col3, col4 = st.columns(4)

    col1.metric("Total Records", total_records)
    col2.metric("High Wage", high_wage)
    col3.metric("Missing SSN", missing_ssn)
    col4.metric("States Covered", states)
