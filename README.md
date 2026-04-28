import streamlit as st

def render_results_table(df):
    st.subheader(f"Results: {len(df)}")

    csv = df.to_csv(index=False).encode("utf-8")

    st.download_button(
        label="📥 Download Results CSV",
        data=csv,
        file_name="tax_search_results.csv",
        mime="text/csv"
    )

    st.dataframe(
        df,
        use_container_width=True,
        hide_index=True
    )
