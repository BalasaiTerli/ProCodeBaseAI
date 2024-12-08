User Authentication System

**Overview**

**This project provides a user authentication system with two core functionalities: User Registration (Sign-up) and User Login. The application is built using Node.js, Express.js, and MongoDB. The system securely stores user credentials and verifies them during login using password hashing.**

**Features**

**User Registration (Sign-up): Allows new users to register by providing an email and password. The password is hashed before storing it in the database.**

**User Login: Allows registered users to log in by verifying their email and password against the stored data.** 
**Email and Password Validation**: Ensures that the email is in a valid format and that the password meets predefined strength requirements.

**Error Handling: Returns appropriate error messages for invalid inputs, such as missing fields, invalid email format, or weak passwords.**

**MongoDB Integration: User data (email and password) is stored in a MongoDB database.**

Technologies Used

**Node.js**: JavaScript runtime for building the application. 
**Express.js**: Web framework to create RESTful APIs. 
**MongoDB**: NoSQL database for storing user data. bcryptjs: Library for hashing passwords securely. 
**dotenv**: For managing environment variables like MongoDB URI and server port. 
**CORS**: Middleware to enable cross-origin requests from different domains. 
**Mongoose**: ODM (Object Data Modeling) library for MongoDB to interact with the database

Setup and Installation

Prerequisites Node.js and npm installed. MongoDB Atlas account (or local MongoDB setup). Installation Steps Clone the repository:

Install dependencies:

npm install

Set up environment variables:

Create a .env file in the root of the project. Add the following configuration:

makefile

Copy code PORT=8000 DB_URI=** Replace with your MongoDB connection string.**

Run the application: npm start The application will be running on the specified port (default: 8000).

Code Functionality

**App Configuration (app.js) 
The app.js file is the entry point of the application. It initializes the Express.js server and connects to MongoDB. It also sets up routes for user registration and login.
Server Setup: Uses express.json() to parse incoming JSON data and cors() for handling cross-origin requests.**

**Route Handlers: 
/signup: POST request for user registration. 
/login: POST request for user login. 
Once the MongoDB connection is established, the server starts listening on the specified port.**

Database Connection (dbConnection.js) The dbConnection.js file is responsible for establishing a connection to the MongoDB database using Mongoose.
Connection: Uses mongoose.connect() to connect to the MongoDB database using the connection string provided in the .env file.

Controllers (signup.js, login.js) There are two controllers for handling user operations: signup and login.
Signup Controller (signup.js)

**Input Validation**: Validates the user’s email and password format using helper functions (validateEmail, validatePassword). Duplicate Email Check: Checks if the email is already registered in the database. Password Hashing: Hashes the user's password using bcryptjs before saving it to the database for security. User Creation: Saves the new user to the MongoDB database. Error Handling: Returns appropriate error messages for invalid inputs, such as missing fields, invalid email format, or weak passwords.

**Login Controller (login.js)**

Input Validation: Ensures that both email and password are provided. Email Check: Checks if the user exists in the database based on the provided email. Password Comparison: Compares the entered password with the hashed password stored in the database using bcryptjs. Login Success/Failure: If the credentials are valid, it returns a success message. Otherwise, it returns an error message indicating invalid credentials.

User Model (userSchema.js) The userSchema.js defines the schema for the user data using Mongoose. The schema includes:
Email: A required and unique string to store the user’s email address. Password: A required string to store the hashed password.

Validation Functions (validation.js) The validation.js file contains helper functions to validate user inputs:
validateEmail(): Ensures that the provided email matches the correct email format using regular expressions. validatePassword(): Ensures that the password meets the following criteria: At least 6 characters long. Contains at least one uppercase letter. Contains at least one number. Contains at least one special character.

Error Handling 400 Bad Request: Used when required fields (email or password) are missing or when validation fails (e.g., invalid email format, weak password). 401 Unauthorized: Returned when the provided credentials (email or password) are incorrect. 500 Server Error: Indicates a problem on the server side, such as a failed database operation.

**Testing the API**

**Signup Endpoint URL: POST /signup** Request Body: json Copy code { "email": "user@example.com", "password": "StrongPassword1!" } Response: Success: 201 Created with a success message. Error: 400 Bad Request with an appropriate error message.

**Login Endpoint URL: POST /login**

**Request Body:**

json 
{ "email": "user@example.com", "password": "StrongPassword1!" }

Response: Success: 200 OK with a success message. 
Error: 401 Unauthorized with an error message if the credentials are invalid.

Security Considerations

**Password Hashing**: Passwords are hashed using bcryptjs before they are stored in the database to prevent storing plain text passwords. Validation: Email and password inputs are validated to ensure they meet basic security requirements.

**Conclusion**

**This project provides a simple and secure authentication system using Node.js, Express.js, and MongoDB. It ensures secure storage of user credentials, provides validation for user input, and handles errors gracefully. The system is extendable and can be modified to include additional features like token-based authentication, email verification, or password reset functionality**
