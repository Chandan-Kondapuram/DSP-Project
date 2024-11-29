Here’s a README.md file for your project. You can save it as README.md in your project folder.

Secure Database System with Query Integrity and Data Confidentiality

Project Description

This project implements a secure database system that ensures data confidentiality, integrity, and access control for multiple user groups. It is designed to:
	•	Authenticate users using hashed passwords.
	•	Protect sensitive data (gender and age) with encryption.
	•	Detect tampered or incomplete query results using integrity checks.
	•	Restrict access based on user roles.

Features

1. User Authentication

	•	Secure user registration and login using bcrypt for password hashing.
	•	Ensures that plaintext passwords are never stored in the database.

2. Role-Based Access Control

	•	Group H: Full access to all database fields and permission to add data.
	•	Group R: Restricted access (cannot view first_name and last_name) and no permission to add data.

3. Query Integrity

	•	Each data record includes a row_hash for tamper detection.
	•	Query results include an overall_hash to ensure completeness.

4. Data Confidentiality

	•	Sensitive fields (gender and age) are encrypted using Fernet.
	•	Prevents exposure of sensitive information even if the database is compromised.

Technologies Used

	•	Backend: Flask
	•	Database: MySQL
	•	Libraries:
	•	bcrypt: Password hashing.
	•	Fernet: Encryption for sensitive fields.
	•	mysql-connector: Database connection.
	•	Language: Python

System Architecture

+---------------------------+
|        User               |
|  (Group H / Group R)      |
+---------------------------+
         |
         | Requests: Registration, Login, Query, Add Data
         v
+---------------------------+
|    Flask Application      |
| - Authentication          |
| - Encryption/Decryption   |
| - Access Control          |
| - Query Integrity Checks  |
+---------------------------+
         |
         | Data Storage: Encrypted Fields, Row Hashes
         v
+---------------------------+
|       MySQL Database      |
| - Encrypted Fields        |
| - Row Hashes for Integrity|
| - Hashed Passwords        |
+---------------------------+

API Endpoints

1. User Registration

	•	Endpoint: /register
	•	Method: POST
	•	Request Body:

{
  "username": "Ronaldo",
  "password": "CR7",
  "group": "H"
}


	•	Response:

{
  "message": "User registered successfully!"
}



2. User Login

	•	Endpoint: /login
	•	Method: POST
	•	Request Body:

{
  "username": "Ronaldo",
  "password": "CR7"
}


	•	Response:

{
  "message": "Login successful!",
  "group": "H"
}



3. Query Data

	•	Endpoint: /query
	•	Method: GET
	•	Query Parameter:
	•	group=H or group=R
	•	Response:

[
  {
    "id": 1,
    "gender": "encrypted_value",
    "age": "encrypted_value",
    "weight": 70.5,
    "height": 180.0,
    "health_history": "No significant health issues"
  }
]



4. Add Data (Group H Only)

	•	Endpoint: /add
	•	Method: POST
	•	Headers:
	•	username: Ronaldo
	•	password: CR7
	•	Request Body:

{
  "first_name": "John",
  "last_name": "Doe",
  "gender": 1,
  "age": 30,
  "weight": 75.5,
  "height": 180,
  "health_history": "No significant health issues"
}


	•	Response:

{
  "message": "Data added successfully!"
}

Setup Instructions

1. Prerequisites

	•	Python 3.8 or above
	•	MySQL database server
	•	Required Python libraries:
	•	bcrypt
	•	cryptography
	•	mysql-connector-python

2. Installation

	1.	Clone the repository:

git clone https://github.com/your-username/secure-database-project.git
cd secure-database-project


	2.	Install dependencies:

pip install -r requirements.txt


	3.	Set up the database:
	•	Run the database_setup.py script to create the database and populate it with dummy data:

python database_setup.py



3. Run the Application

Start the Flask application:

python app.py

Testing

1. Registration

	•	Test successful and failed registrations.
	•	Verify the users table in the database.

2. Login

	•	Test successful and failed login attempts.

3. Query Data

	•	Test outputs for Group H (full access) and Group R (restricted access).

4. Add Data

	•	Test successful and unauthorized attempts to add data.

5. Query Integrity

	•	Modify data manually in the database and test tampered query detection.

Limitations

	1.	Key Management: The encryption key is stored locally (cipher.key), making it a single point of failure.
	2.	Query Completeness: The overall_hash mechanism may not fully prevent missing record attacks.
	3.	Performance Overhead: Encryption, decryption, and hashing operations can slow down queries as data grows.

License

This project is licensed under the MIT License.

You can save this content as README.md in your project folder, and Git will automatically display it on your repository’s main page. Let me know if you need any further assistance! 😊
