import streamlit as st
import pandas as pd

st.set_page_config(
    page_title="Tax Search Dashboard",
    page_icon="📊",
    layout="wide"
)

# ---------------------------
# Sample Data
# ---------------------------
data = [
    {
        "ClientName": "Susan Thomas",
        "EmployerName": "TechStart Inc",
        "FormType": "1099-NEC",
        "TaxYear": "2022",
        "State": "Florida",
        "Wages": 97937.42,
        "SSN": "655-72-2057",
        "AmendedReturns": 11
    },
    {
        "ClientName": "John Smith",
        "EmployerName": "Acme Corp",
        "FormType": "W-2",
        "TaxYear": "2021",
        "State": "California",
        "Wages": 120000,
        "SSN": "",
        "AmendedReturns": 0
    },
    {
        "ClientName": "Maria Lee",
        "EmployerName": "",
        "FormType": "1099-MISC",
        "TaxYear": "2022",
        "State": "Texas",
        "Wages": 65000,
        "SSN": "111-22-3333",
        "AmendedReturns": 2
    }
]

df = pd.DataFrame(data)

# ---------------------------
# Flags
# ---------------------------
def make_flags(row):
    flags = []

    if row["SSN"] == "":
        flags.append("Missing SSN")

    if row["EmployerName"] == "":
        flags.append("Missing Employer")

    if row["Wages"] > 100000:
        flags.append("High Wage")

    if row["AmendedReturns"] > 5:
        flags.append("High Amendments")

    return ", ".join(flags) if flags else "None"

df["Flags"] = df.apply(make_flags, axis=1)

# Replace empty values
df = df.replace("", "N/A")

# ---------------------------
# UI
# ---------------------------
st.title("📊 Tax Search Dashboard")
st.caption("Smart search for tax filing records")

query = st.text_input(
    "Search by client, employer, state, or phrase"
)

c1, c2, c3, c4 = st.columns(4)

year = c1.selectbox("Year", ["All"] + sorted(df["TaxYear"].unique().tolist()))
form = c2.selectbox("Form", ["All"] + sorted(df["FormType"].unique().tolist()))
state = c3.selectbox("State", ["All"] + sorted(df["State"].unique().tolist()))
flag = c4.selectbox(
    "Flags",
    ["All", "Missing SSN", "Missing Employer", "High Wage", "High Amendments"]
)

# ---------------------------
# Filter Logic
# ---------------------------
filtered = df.copy()

if query:
    q = query.lower()
    filtered = filtered[
        filtered.astype(str).apply(
            lambda row: row.str.lower().str.contains(q).any(),
            axis=1
        )
    ]

if year != "All":
    filtered = filtered[filtered["TaxYear"] == year]

if form != "All":
    filtered = filtered[filtered["FormType"] == form]

if state != "All":
    filtered = filtered[filtered["State"] == state]

if flag != "All":
    filtered = filtered[
        filtered["Flags"].str.contains(flag, case=False)
    ]

# ---------------------------
# Output
# ---------------------------
st.subheader(f"Results: {len(filtered)}")

st.dataframe(
    filtered,
    use_container_width=True,
    hide_index=True
)
