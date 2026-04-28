def get_mock_data():
    return [
        {
            "ClientName": "Susan Thomas",
            "EmployerName": "TechStart Inc",
            "FormType": "1099-NEC",
            "TaxYear": 2022,
            "State": "Florida",
            "Wages": 97937.42,
            "SSN": "655-72-2057",
            "AmendedReturns": 11,
            "Flags": "High Amendments"
        },
        {
            "ClientName": "John Smith",
            "EmployerName": "Acme Corp",
            "FormType": "W-2",
            "TaxYear": 2021,
            "State": "California",
            "Wages": 120000,
            "SSN": "N/A",
            "AmendedReturns": 0,
            "Flags": "Missing SSN, High Wage"
        },
        {
            "ClientName": "Maria Lee",
            "EmployerName": "N/A",
            "FormType": "1099-MISC",
            "TaxYear": 2022,
            "State": "Texas",
            "Wages": 65000,
            "SSN": "111-22-3333",
            "AmendedReturns": 2,
            "Flags": "Missing Employer"
        }
    ]
