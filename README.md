import streamlit as st

def render_filters(df):
    years = ["All"] + sorted(df["TaxYear"].astype(str).unique().tolist())
    forms = ["All"] + sorted(df["FormType"].unique().tolist())
    states = ["All"] + sorted(df["State"].unique().tolist())
    flags = ["All"] + sorted(df["Flags"].unique().tolist())

    col1, col2, col3, col4 = st.columns(4)

    with col1:
        year = st.selectbox("Year", years)

    with col2:
        form = st.selectbox("Form", forms)

    with col3:
        state = st.selectbox("State", states)

    with col4:
        flag = st.selectbox("Flags", flags)

    return year, form, state, flag
