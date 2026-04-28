import streamlit as st
import pandas as pd
from services.mock_data import get_mock_data
from components.filters import render_filters

# ---------------------------------------------------
# Page Config
# ---------------------------------------------------
st.set_page_config(
    page_title="Tax Search Dashboard",
    page_icon="📊",
    layout="wide",
    initial_sidebar_state="expanded"
)

# ---------------------------------------------------
# Title
# ---------------------------------------------------
st.title("📊 Tax Search Dashboard")
st.caption("Smart search for tax filing records")

# ---------------------------------------------------
# Load Data
# ---------------------------------------------------
data = get_mock_data()
df = pd.DataFrame(data)

# ---------------------------------------------------
# Search Bar
# ---------------------------------------------------
query = st.text_input("Search by client, employer, state, or phrase")

# ---------------------------------------------------
# Filters
# ---------------------------------------------------
year, form, state, flag = render_filters(df)

# ---------------------------------------------------
# Filtering Logic
# ---------------------------------------------------
filtered = df.copy()

# Search filter
if query:
    filtered = filtered[
        filtered.astype(str).apply(
            lambda row: row.str.contains(query, case=False).any(),
            axis=1
        )
    ]

# Year filter
if year != "All":
    filtered = filtered[filtered["TaxYear"].astype(str) == year]

# Form filter
if form != "All":
    filtered = filtered[filtered["FormType"] == form]

# State filter
if state != "All":
    filtered = filtered[filtered["State"] == state]

# Flag filter
if flag != "All":
    filtered = filtered[filtered["Flags"] == flag]

# ---------------------------------------------------
# Results
# ---------------------------------------------------
st.subheader(f"Results: {len(filtered)}")
st.dataframe(filtered, use_container_width=True, hide_index=True)
