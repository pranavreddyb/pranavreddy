import streamlit as st

from pages.dashboard import show_dashboard
from pages.analytics import show_analytics
from pages.test_harness import show_test_harness

# ---------------- Page Config ----------------
st.set_page_config(
    page_title="Tax Search Dashboard",
    page_icon="📊",
    layout="wide"
)

# ---------------- Hide Default Streamlit Pages Nav ----------------
st.markdown("""
<style>
[data-testid="stSidebarNav"] {
    display: none;
}
</style>
""", unsafe_allow_html=True)

# ---------------- Load Custom CSS ----------------
try:
    with open("assets/style.css") as f:
        st.markdown(f"<style>{f.read()}</style>", unsafe_allow_html=True)
except:
    pass

# ---------------- Sidebar Navigation ----------------
st.sidebar.title("Navigation")

page = st.sidebar.radio(
    "Go to",
    ["Dashboard", "Analytics", "Test Harness"]
)

# ---------------- Route Pages ----------------
if page == "Dashboard":
    show_dashboard()

elif page == "Analytics":
    show_analytics()

elif page == "Test Harness":
    show_test_harness()
