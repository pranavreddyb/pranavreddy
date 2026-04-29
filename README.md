/* App background */
.stApp {
    background: #f8fafc;
    color: #111827;
    font-family: 'Segoe UI', sans-serif;
}

/* Sidebar */
section[data-testid="stSidebar"] {
    width: 260px !important;
    background: #111827;
    color: white;
}

section[data-testid="stSidebar"] * {
    color: white !important;
}

/* Title spacing */
h1 {
    font-size: 42px !important;
    font-weight: 700 !important;
    margin-bottom: 0.3rem !important;
}

/* Inputs */
input, .stSelectbox div[data-baseweb="select"] {
    border-radius: 12px !important;
}

/* Metric cards */
[data-testid="metric-container"] {
    background: white;
    border: 1px solid #e5e7eb;
    padding: 18px;
    border-radius: 16px;
    box-shadow: 0 4px 14px rgba(0,0,0,0.05);
}

/* Buttons */
.stButton button, .stDownloadButton button {
    background: linear-gradient(90deg,#2563eb,#1d4ed8);
    color: white;
    border: none;
    border-radius: 10px;
    padding: 0.6rem 1rem;
    font-weight: 600;
}

/* Dataframe */
[data-testid="stDataFrame"] {
    background: white;
    border-radius: 14px;
    padding: 8px;
    border: 1px solid #e5e7eb;
}

/* Reduce top padding */
.block-container {
    padding-top: 2rem;
}
