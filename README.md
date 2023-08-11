# Interview Scheduler API

## Introduction
This is the backend server for [Scheduler project](https://github.com/IrinaGM/scheduler)
## Setup
1. Clone this repository [here](https://github.com/IrinaGM/scheduler-api)
2. Install dependencies with `npm install`

## Creating The DB
##### Setting up development env:

1. **MUST** Run on your **vagrant** terminal:
   To login to the PostgreSQL server with the **username** `development` and the **password** `development` use the following command:
   `psql -U development`

2. Create a database using the command `CREATE DATABASE scheduler_development;`.

3. Create `.env.development` file and fill in the necessary PostgreSQL configuration. The `node-postgres` library uses these environment variables by default.
   ```
   PGHOST=localhost
   PGUSER=development
   PGDATABASE=scheduler_development
   PGPASSWORD=development
   PGPORT=5432
   ```

##### Setting up test env:

1. **MUST** Run on your **vagrant** terminal:
   To login to the PostgreSQL server with the username `development` and the password `development` use the following command:
   `psql -U development`

2. Create a database with the command `CREATE DATABASE scheduler_test;`.

3. create `.env.test` file and fill in the necessary PostgreSQL configuration:
   ```
   PGHOST=localhost
   PGUSER=development
   PGDATABASE=scheduler_test
   PGPASSWORD=development
   PGPORT=5432
   ```

## Seeding the Development server

Run the development server with `npm start` in the Host environment.

Run **one** of the following commands, as they result in the same thing:

- Make a `GET` request to `/api/debug/reset` with `curl http://localhost:8001/api/debug/reset`.
  **OR**
- Use the browser to navigate to `http://localhost:8001/api/debug/reset`.

The `development` data is random. Each time we seed we expect to see different appointments.

## Run The Server

Running the server normally

```sh
npm start
```

Running the server in error mode, so it returns an error when saving/deleting for testing the client's error handling capabilities

```sh
npm run error
```

Running the server in test mode:

```sh
npm run test:server
```

## API

### Days

`GET /api/days`

Response

```json
[
  {
    "id": 1,
    "name": "Monday",
    "appointments": [1, 2],
    "interviewers": [1, 2],
    "spots": 0
  }
]
```

### Appointments

`GET /api/appointments`

Response:

```json
{
  "1": {
    "id": 1,
    "time": "12pm",
    "interview": {
      "student": "Lydia Miller-Jones",
      "interviewer": 1
    }
  },
  "2": {
    "id": 2,
    "time": "1pm",
    "interview": {
      "student": "Archie Cohen",
      "interviewer": 2
    }
  }
}
```

`PUT /api/appointments/:id`

Body:

```json
{
  "interview": {
    "student": String,
    "interviewer": Number
  }
}
```

`DELETE /api/appointments/:id`

### Interviewers

`GET /api/interviewers`

Response:

```json
{
  "1": {
    "id": 1,
    "name": "Sylvia Palmer",
    "avatar": "https://i.imgur.com/LpaY82x.png"
  },
  "2": {
    "id": 2,
    "name": "Tori Malcolm",
    "avatar": "https://i.imgur.com/Nmx0Qxo.png"
  }
}
```
