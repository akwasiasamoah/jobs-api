# Job Management Application

This application provides functionality for user authentication and job management. It allows users to register, log in, and manage their job listings. The application is built using Node.js with Express and MongoDB.

## Features

- **User Authentication:**

  - Register a new user.
  - Log in to an existing account.
  - JWT-based authentication for secure access.

- **Job Management:**
  - Create a new job listing.
  - View all job listings created by the user.
  - View details of a specific job listing.
  - Update job details.
  - Delete a job listing.

## Requirements

- Node.js (v14 or higher)
- MongoDB (or a cloud MongoDB service like MongoDB Atlas)
- Postman (for API testing)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/akwasiasamoah/jobs-api.git
   ```

2. Install dependencies:

   ```bash
   cd job-api
   npm install
   ```

3. Set up environment variables:

   - Create a `.env` file in the root of the project and add the following variables:
     ```env
     MONGO_URI=<your-mongo-db-uri>
     JWT_SECRET=<your-jwt-secret>
     JWT_LIFETIME=<your-jwt-lifetime>
     ```

4. Start the application:

   ```bash
   npm start
   ```

   The server will be running at `http://localhost:5000`.

## API Endpoints

### Authentication

#### POST `/api/v1/auth/register`

Registers a new user.

**Request body:**

```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "password": "password123"
}
```

**Response:**

```json
{
  "user": {
    "name": "John Doe"
  },
  "token": "<JWT_TOKEN>"
}
```

#### POST `/api/v1/auth/login`

Logs in an existing user.

**Request body:**

```json
{
  "email": "johndoe@example.com",
  "password": "password123"
}
```

**Response:**

```json
{
  "user": {
    "name": "John Doe"
  },
  "token": "<JWT_TOKEN>"
}
```

### Job Management

#### GET `/api/v1/jobs`

Fetches all jobs created by the authenticated user.

**Response:**

```json
{
  "jobs": [
    {
      "_id": "job-id",
      "company": "Company Name",
      "position": "Software Engineer",
      "status": "pending",
      "createdBy": "user-id",
      "createdAt": "2024-12-23T00:00:00.000Z",
      "updatedAt": "2024-12-23T00:00:00.000Z"
    }
  ],
  "count": 1
}
```

#### GET `/api/v1/jobs/:id`

Fetches a specific job listing by its ID.

**Response:**

```json
{
  "job": {
    "_id": "job-id",
    "company": "Company Name",
    "position": "Software Engineer",
    "status": "pending",
    "createdBy": "user-id",
    "createdAt": "2024-12-23T00:00:00.000Z",
    "updatedAt": "2024-12-23T00:00:00.000Z"
  }
}
```

#### POST `/api/v1/jobs`

Creates a new job listing.

**Request body:**

```json
{
  "company": "Company Name",
  "position": "Software Engineer",
  "status": "pending"
}
```

**Response:**

```json
{
  "job": {
    "_id": "job-id",
    "company": "Company Name",
    "position": "Software Engineer",
    "status": "pending",
    "createdBy": "user-id",
    "createdAt": "2024-12-23T00:00:00.000Z",
    "updatedAt": "2024-12-23T00:00:00.000Z"
  }
}
```

#### PUT `/api/v1/jobs/:id`

Updates a specific job listing.

**Request body:**

```json
{
  "company": "Updated Company Name",
  "position": "Senior Software Engineer",
  "status": "interview"
}
```

**Response:**

```json
{
  "job": {
    "_id": "job-id",
    "company": "Updated Company Name",
    "position": "Senior Software Engineer",
    "status": "interview",
    "createdBy": "user-id",
    "createdAt": "2024-12-23T00:00:00.000Z",
    "updatedAt": "2024-12-23T00:00:00.000Z"
  }
}
```

#### DELETE `/api/v1/jobs/:id`

Deletes a specific job listing.

**Response:**

```json
{
  "message": "Job deleted successfully"
}
```

## Models

### User Model

The `User` model stores information about a user, including their name, email, and password. Passwords are hashed using `bcryptjs` before storing.

#### Fields:

- `name`: The user's name (string).
- `email`: The user's email (string).
- `password`: The user's password (string).

### Job Model

The `Job` model stores job listings created by users.

#### Fields:

- `company`: The name of the company (string).
- `position`: The job position (string).
- `status`: The job's status (string, one of `interview`, `declined`, `pending`).
- `createdBy`: The ID of the user who created the job (ObjectId).

## Error Handling

The application uses custom error classes for various error scenarios:

- **BadRequestError**: Thrown for invalid requests.
- **UnauthenticatedError**: Thrown when authentication fails.
- **NotFoundError**: Thrown when a job is not found.

## Conclusion

This application provides basic functionality for user authentication and job management. It can be easily extended to include additional features, such as job categorization, notifications, or advanced user roles.
