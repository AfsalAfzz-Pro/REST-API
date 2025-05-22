# CSV Data Processing API

This Django REST Framework API allows for uploading, validating, and processing user data from CSV files.

## Features

- API endpoint for uploading CSV files containing user data
- Validation of user data according to specified rules
- Detailed error reporting for invalid records
- Handling of duplicate email addresses
- Unit tests for all functionality

## Requirements

- Python 3.8+
- Django 5.2+
- Django REST Framework

## Installation and Setup

1. Clone the repository
2. Create a virtual environment:
   ```
   python -m venv env
   .\env\Scripts\activate  # Windows
   ```
3. Install dependencies:
   ```
   pip install django djangorestframework
   ```
4. Apply migrations:
   ```
   python manage.py makemigrations
   python manage.py migrate
   ```
5. Run the development server:
   ```
   python manage.py runserver
   ```

## API Endpoints

### Upload CSV
- URL: `/api/csv/upload/`
- Method: POST
- Content-Type: multipart/form-data
- Parameter: `file` (CSV file)

### Sample CSV Format
```
name,email,age
John Doe,john.doe@example.com,35
Jane Smith,jane.smith@example.com,28
```

### Validation Rules
- `name`: Must be a non-empty string
- `email`: Must be a valid email address
- `age`: Must be an integer between 0 and 120

## Running Tests

Run unit tests with the following command:
```
python manage.py test core
```

## Sample Output

A successful API response will return:
```json
{
  "total_records_saved": 2,
  "total_records_rejected": 1,
  "rejected_records": [
    {
      "row": 3,
      "data": {"name": "Invalid User", "email": "", "age": "200"},
      "errors": {
        "email": ["This field may not be blank."],
        "age": ["Ensure this value is less than or equal to 120."]
      }
    }
  ]
}
``` 