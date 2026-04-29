import streamlit as st
import pandas as pd
import plotly.express as px
from services.mock_data import get_mock_data

def show_analytics():
    st.title("📈 Analytics")
    st.caption("Visual insights from tax records")

    df = pd.DataFrame(get_mock_data())

    chart1 = px.bar(
        df.groupby("State")["Wages"].sum().reset_index(),
        x="State",
        y="Wages",
        title="Total Wages by State"
    )

    chart2 = px.pie(
        df,
        names="FormType",
        title="Form Type Distribution"
    )

    st.plotly_chart(chart1, use_container_width=True)
    st.plotly_chart(chart2, use_container_width=True)
