import streamlit as st

def render_results_table(df):
    st.subheader(f"Results: {len(df)}")
    st.dataframe(
        df,
        use_container_width=True,
        hide_index=True
    )
