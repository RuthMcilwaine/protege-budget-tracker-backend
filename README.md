
# Protege Budget Tracker — Backend API

## Repository  
[github.com/RuthMcilwaine/backend-Protege-Budget-Tracker](https://github.com/RuthMcilwaine/backend-Protege-Budget-Tracker)


## Project Overview  
This backend API supports the Protege Budget Tracker app, which allows a manager to track proteges' learning budgets, their expenses, and budget balances. It is built with Node.js, Express, and MongoDB, providing RESTful endpoints for managing proteges and their purchased items.


## Table of Contents  
- [Tech Stack](#tech-stack)  
- [Setup & Deployment](#setup--deployment)  
- [API Overview](#api-overview)  
  - [Items Purchased API](#items-purchased-api-apiitems)  
  - [Proteges API](#proteges-api-apiproteges)  
- [Database Models](#database-models)  
- [Testing](#testing)  
- [Project Notes](#project-notes)  
- [Contact](#contact)  
- [Related Repositories](#related-repositories)


## Tech Stack  
- **Backend Framework:** Node.js, Express  
- **Database:** MongoDB with Mongoose ODM  
- **Deployment:** Now (Vercel)  
- **Tools:** Git, Postman (recommended for testing), VS Code  


## Setup & Deployment

1. Clone the repository:  
   ```bash
   git clone https://github.com/ruthmci/backend-Protege-Budget-Tracker.git
   cd backend-Protege-Budget-Tracker
    ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Configure environment variables:
   Create a `.env` file with your MongoDB connection string and other necessary configs.

4. Run the server locally:

   ```bash
   npm start
   ```

5. Deployment:
   Use the `now` CLI to deploy:

   ```bash
   now
   ```

## API Overview

### Items Purchased API (`/api/items`)

| HTTP Method | Endpoint                | Description                       |
| ----------- | ----------------------- | --------------------------------- |
| GET         | `/api/items/`           | Retrieve all purchased items      |
| GET         | `/api/items/hello`      | Test route, returns "api working" |
| POST        | `/api/items/add`        | Add a new purchased item          |
| GET         | `/api/items/:id`        | Get one item by ID                |
| DELETE      | `/api/items/:id`        | Delete one item by ID             |
| PATCH       | `/api/items/update/:id` | Update one item by ID             |

**Request Body Example for Adding or Updating an Item:**

```json
{
  "protegeId": "string",           // ID of the protege
  "description": "string",         // Description of the item
  "expenditure": 100.50,           // Amount spent (number)
  "date": "YYYY-MM-DD"             // Date of purchase (string)
}
```


### Proteges API (`/api/proteges`)

| HTTP Method | Endpoint                   | Description                            |
| ----------- | -------------------------- | -------------------------------------- |
| GET         | `/api/proteges/`           | Retrieve all proteges with their items |
| GET         | `/api/proteges/:id`        | Get one protege with related items     |
| POST        | `/api/proteges/add`        | Add a new protege                      |
| DELETE      | `/api/proteges/:id`        | Delete a protege by ID                 |
| PATCH       | `/api/proteges/update/:id` | Update a protege by ID                 |

**Request Body Example for Adding or Updating a Protege:**

```json
{
  "protegename": "string",       // Name of the protege
  "protegeemail": "string",      // Protege's email (must be unique)
  "expenditure": 100,            // Total expenditure (number)
  "balance": 900,                // Remaining budget balance (number)
  "date": "YYYY-MM-DD"           // Date (string)
}
```

## Database Models

* **Protege Model** — stores protege details like name, email, expenditure, balance, and date.
* **Item Model** — stores purchased items linked to proteges by `protege_id`.

The API returns proteges alongside their related purchased items for convenience.

## Testing

* Use tools like Postman or Insomnia to test the API endpoints.
* The route `/api/items/hello` can be used to verify the API is up (`GET` request returns "api working").
* Validation errors return HTTP status 400 with detailed error messages.

## Project Notes

* Unique constraint on `protegeemail` prevents duplicates; duplicate submissions will return an error message.
* The backend is designed to serve the frontend app, which aggregates protege data with related items.
* Data validation and error handling are implemented for smooth client interaction.

## Related Repositories

- Frontend Repo: [github.com/RuthMcilwaine/frontend-Protege-Budget-Tracker](https://github.com/RuthMcilwaine/frontend-Protege-Budget-Tracker)