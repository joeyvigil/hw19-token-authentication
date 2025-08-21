# hw19-token-authentication
*For practice implement token authentication for your Mechanic shop*

-   Create an encode_token function that takes in a mechanic_id to create a token specific to that user.
-   add a password field to you Mechanics model. (Drop all tables using db.drop_all())
-   login_schema, which can be made by excluding all fields except email and password from your MechanicSchema
-   In your mechanics blueprint, create a login route:
-   POST '/login' : passing in email and password, validated by login_schema
```json
method: POST
url: http://127.0.0.1:5000/mechanics/login
body (raw):
{
    "email": "name@email.com",
    "password": "password"
}
response:
{
    "message": "Hello There james1",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NTU4MTE5MzgsImlhdCI6MTc1NTgwODMzOCwic3ViIjoiMiJ9.9_JzRCvOFlzhfguR_OsPYjJo4TCTTKKvGuc4HBiT3Gg"
}
```
-   After credentials have been validate utilizes the encode_token() function to make a token to be returned to that customer.
```json
method: GET
url: http://127.0.0.1:5000/mechanics/profile
authorization (bearer token): eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NTU4MTE5MzgsImlhdCI6MTc1NTgwODMzOCwic3ViIjoiMiJ9.9_JzRCvOFlzhfguR_OsPYjJo4TCTTKKvGuc4HBiT3Gg
response:
{
    "address": "1990 W Philly Ave1",
    "email": "name@email.com",
    "first_name": "james1",
    "id": 2,
    "last_name": "thorton1",
    "password": "scrypt:32768:8:1$48RhCUSV5KvGJ6de$ec443302a2ec63e503389cc94330795ad46aa05bb01ffccdabdfec8ada272311ea3e6847be1b2c3ad7ad42edd2ec8a5e0c00619e1c4661412590d9e2c3e7e00d",
    "salary": 1000000.0
}
```

Create @token_required wrapper, that validates and unpacks the token, and stores the id in the request as a field. Create a route that requires a token, that returns the service_tickets related to that mechanic.

-   GET '/my-tickets': requires a Bearer Token authorization. **(OPTIONAL... for now will be required in the end project)**
-   The route function should extract the mechanic_id from the request.
-   Using that id query the service_tickets that belong to the mechanic.

Additionally add @token_required to any routes you think should require authorization. (ex: Update, Delete,...)