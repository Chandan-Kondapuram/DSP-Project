# Secure Database System with Query Integrity and Data Confidentiality

## Project Description
This project implements a secure database system that ensures data confidentiality, integrity, and access control for multiple user groups. It is designed to:
- Authenticate users using hashed passwords.
- Protect sensitive data (`gender` and `age`) with encryption.
- Detect tampered or incomplete query results using integrity checks.
- Restrict access based on user roles.

The system provides endpoints for:
- User registration and authentication.
- Querying and adding data.
- Ensuring integrity and confidentiality for sensitive information.

---

## Features
1. User Authentication:
   - Secure registration and login with `bcrypt` for password hashing.
   - Passwords are stored in a hashed format, ensuring security.

2. Role-Based Access Control:
   - **Group H**: Full access to all fields in the database and permission to add data.
   - **Group R**: Restricted access (no access to `first_name` and `last_name`) and no permission to add data.

3. Query Integrity:
   - Uses `row_hash` for individual record integrity and `overall_hash` for completeness verification.

4. Data Confidentiality:
   - Encrypts sensitive fields (`gender`, `age`) using `Fernet`.

5. Tamper Detection:
   - Detects any modification of data or missing records in query results.

---

## Technologies Used
- Backend Framework: Flask - Used for building the RESTful API and handling user requests.
- Database: MySQL - Serves as the database for storing user credentials, encrypted fields, and healthcare data.
- Security Libraries:
  - `bcrypt`: Ensures secure password hashing and storage.
  - `Fernet` (from the `cryptography` library): Provides encryption and decryption for sensitive fields (`gender` and `age`).
- Database Connector: `mysql-connector-python` - Facilitates communication between the Flask application and the MySQL database.
- Language: Python - Provides the flexibility and libraries required for secure application development.
- Development Tools:
  - `curl`: For testing RESTful API endpoints.
  - Postman (optional): For interactive API testing.

---

## Setup Instructions

### Prerequisites
- Software Requirements:
  - Python 3.8 or above.
  - MySQL database server (installed and running).
- Python Libraries:
  Install the required libraries using:
  ```bash
  pip install -r requirements.txt

Installation Steps

1.Clone the repository:

git clone https://github.com/your-username/secure-database-project.git

cd secure-database-project

2.Initialize the database:

•Run the database\_setup.py script to create the database and tables, and populate them with sample data:

python database\_setup.py

3.Run the Flask application:

python app.py

4.Test the application:

•Use curl or Postman to send requests to the API endpoints.

API Endpoints

User Registration

•Endpoint: /register

•Method: POST

•Example Request:

curl -X POST http://127.0.0.1:5000/register \\

\-H "Content-Type: application/json" \\

\-d '{"username": "Ronaldo", "password": "CR7", "group": "H"}'

•Example Response:

{

  "message": "User registered successfully!"

}

User Login**

•Endpoint: /login

•Method**: POST

•Example Request:

curl -X POST http://127.0.0.1:5000/login \\

\-H "Content-Type: application/json" \\

\-d '{"username": "Ronaldo", "password": "CR7"}'

•Example Response:

{

  "message": "Login successful!",

  "group": "H"

}

Query Data

•Endpoint: /query

•**Method**: GET

•**Query Parameter**:

•group=H or group=R.

•Example Request:

curl -X GET "http://127.0.0.1:5000/query?group=H"

•Example Response:

\[

  {

    "id": 1,

    "gender": "encrypted\_value",

    "age": "encrypted\_value",

    "weight": 70.5,

    "height": 180.0,

    "health\_history": "No significant health issues"

  }

\]

Add Data (Group H Only)

•Endpoint: /add

•Method: POST

•Headers:

•username: Ronaldo

•password: CR7.

•Example Request:

curl -X POST http://127.0.0.1:5000/add \\

\-H "Content-Type: application/json" \\

\-H "username: Ronaldo" -H "password: CR7" \\

\-d '{"first\_name": "John", "last\_name": "Doe", "gender": 1, "age": 30, "weight": 75.5, "height": 180, "health\_history": "No issues"}'

•Example Response:

{

  "message": "Data added successfully!"

}

Testing and Results

Feature Testing:

1.Registration:

•Registered users with valid and invalid data.

•Verified hashed passwords in the database.

2.Login:

•Tested with correct and incorrect credentials.

3.Query Data:

•Group H: Retrieved full data.

•Group R: Verified restricted access.

4.Add Data:

•Verified that only Group H users can add data.

5.Tamper Detection:

•Modified database records and confirmed detection of integrity failures.

Limitations and Suggestions

1.Key Management:

•The encryption key (cipher.key) is stored locally. A more robust solution would use a key management system (e.g., AWS KMS or Azure Key Vault).

2.Performance:

•Encryption and hashing add overhead, which could slow performance for larger datasets.

3.Password Policy:

•Currently, no policy enforces strong passwords. Implementing password complexity requirements could enhance security.

4.Error Handling:

•Improve error messages for more descriptive feedback to users.
