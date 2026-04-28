import streamlit as st
import pandas as pd
import plotly.express as px
from services.mock_data import get_mock_data

st.set_page_config(page_title="Analytics", layout="wide")

st.title("📈 Analytics Dashboard")
st.caption("Insights from tax filing records")

# Load data
data = get_mock_data()
df = pd.DataFrame(data)

# -----------------------------
# Chart 1: Records by State
# -----------------------------
state_counts = df["State"].value_counts().reset_index()
state_counts.columns = ["State", "Count"]

fig1 = px.bar(
    state_counts,
    x="State",
    y="Count",
    title="Records by State"
)

# -----------------------------
# Chart 2: Records by Form Type
# -----------------------------
form_counts = df["FormType"].value_counts().reset_index()
form_counts.columns = ["FormType", "Count"]

fig2 = px.pie(
    form_counts,
    names="FormType",
    values="Count",
    title="Form Type Distribution"
)

# -----------------------------
# Chart 3: Wages by Client
# -----------------------------
fig3 = px.bar(
    df,
    x="ClientName",
    y="Wages",
    title="Wages by Client"
)

# -----------------------------
# Layout
# -----------------------------
col1, col2 = st.columns(2)

with col1:
    st.plotly_chart(fig1, use_container_width=True)

with col2:
    st.plotly_chart(fig2, use_container_width=True)

st.plotly_chart(fig3, use_container_width=True)
