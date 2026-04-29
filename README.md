/* Global */
.stApp {
    background: linear-gradient(180deg,#f8fafc,#eef2ff);
    font-family: "Segoe UI", sans-serif;
    color: #111827;
}

.block-container {
    padding-top: 1.5rem;
    padding-left: 2rem;
    padding-right: 2rem;
}

/* Sidebar */
section[data-testid="stSidebar"] {
    background: linear-gradient(180deg,#0f172a,#111827);
    width: 260px !important;
}

section[data-testid="stSidebar"] * {
    color: white !important;
}

section[data-testid="stSidebar"] .stRadio label {
    padding: 8px 10px;
    border-radius: 10px;
}

/* Headings */
h1 {
    font-size: 42px !important;
    font-weight: 800 !important;
    color: #0f172a !important;
    margin-bottom: 0.2rem !important;
}

h2, h3 {
    color: #111827 !important;
}

/* Inputs */
.stTextInput input,
.stSelectbox div[data-baseweb="select"] {
    border-radius: 12px !important;
    border: 1px solid #dbeafe !important;
    background: white !important;
}

/* Metric cards */
[data-testid="metric-container"] {
    background: rgba(255,255,255,0.85);
    border: 1px solid rgba(255,255,255,0.4);
    backdrop-filter: blur(8px);
    border-radius: 18px;
    padding: 18px;
    box-shadow: 0 8px 24px rgba(15,23,42,0.08);
}

/* Buttons */
.stButton button,
.stDownloadButton button {
    border: none !important;
    border-radius: 12px !important;
    background: linear-gradient(90deg,#2563eb,#1d4ed8) !important;
    color: white !important;
    font-weight: 700 !important;
    padding: 0.65rem 1rem !important;
}

/* Dataframe */
[data-testid="stDataFrame"] {
    background: white;
    border-radius: 16px;
    border: 1px solid #e5e7eb;
    padding: 8px;
    box-shadow: 0 8px 24px rgba(0,0,0,0.04);
}

/* Labels */
label, .stCaption {
    color: #475569 !important;
}
