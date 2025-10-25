# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.

## Admin Mode (teacher-only registration)

This project supports a simple "admin mode" where teachers can register and
unregister students. For now this uses HTTP Basic auth with credentials stored
in `src/teachers.json`.

To use admin endpoints:

1. Edit `src/teachers.json` and add teacher credentials (username/password).
2. Use HTTP Basic auth when calling the signup or unregister endpoints. For
   example, with curl:

```bash
curl -u teacher:password123 -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=student@mergington.edu"
```

Note: This is a simple development convenience. For production, replace this
with a proper authentication system and hashed passwords.

