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
1. **User Authentication**:
   - Secure registration and login with `bcrypt` for password hashing.
   - Passwords are stored in a hashed format, ensuring security.

2. **Role-Based Access Control**:
   - **Group H**: Full access to all fields in the database and permission to add data.
   - **Group R**: Restricted access (no access to `first_name` and `last_name`) and no permission to add data.

3. **Query Integrity**:
   - Uses `row_hash` for individual record integrity and `overall_hash` for completeness verification.

4. **Data Confidentiality**:
   - Encrypts sensitive fields (`gender`, `age`) using `Fernet`.

5. **Tamper Detection**:
   - Detects any modification of data or missing records in query results.

---

## Technologies Used
- **Backend Framework**: Flask - Used for building the RESTful API and handling user requests.
- **Database**: MySQL - Serves as the database for storing user credentials, encrypted fields, and healthcare data.
- **Security Libraries**:
  - `bcrypt`: Ensures secure password hashing and storage.
  - `Fernet` (from the `cryptography` library): Provides encryption and decryption for sensitive fields (`gender` and `age`).
- **Database Connector**: `mysql-connector-python` - Facilitates communication between the Flask application and the MySQL database.
- **Language**: Python - Provides the flexibility and libraries required for secure application development.
- **Development Tools**:
  - `curl`: For testing RESTful API endpoints.
  - Postman (optional): For interactive API testing.

---

## Setup Instructions

### Prerequisites
- **Software Requirements**:
  - Python 3.8 or above.
  - MySQL database server (installed and running).
- **Python Libraries**:
  Install the required libraries using:
  ```bash
  pip install -r requirements.txt
