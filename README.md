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

# Home
@app.get("/")
def home():
    return {"message": "FastAPI is running"}

# GET all employees
@app.get("/employees")
def get_employees():
    return employees

# ADD employee
@app.post("/employees")
def add_employee(employee: dict):
    employees.append(employee)
    return {"message": "Employee added"}

# UPDATE employee
@app.put("/employees/{id}")
def update_employee(id: int, employee: dict):
    if id < len(employees):
        employees[id] = employee
        return {"message": "Employee updated"}
    return {"error": "Invalid ID"}

# DELETE employee
@app.delete("/employees/{id}")
def delete_employee(id: int):
    if id < len(employees):
        employees.pop(id)
        return {"message": "Employee deleted"}
    return {"error": "Invalid ID"}
