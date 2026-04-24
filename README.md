from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:4200"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

employees = []

@app.get("/")
def home():
    return {"message": "FastAPI is running"}

@app.get("/employees")
def get_employees():
    return employees

@app.post("/employees")
def add_employee(employee: dict):
    employees.append(employee)
    return {"message": "Employee added"}
