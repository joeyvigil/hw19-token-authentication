# hw19-token-authentication
*For practice implement token authentication for your Mechanic shop*

-   Create an encode_token function that takes in a mechanic_id to create a token specific to that user.
-   add a password field to you Mechanics model. (Drop all tables using db.drop_all())
-   login_schema, which can be made by excluding all fields except email and password from your MechanicSchema
-   In your mechanics blueprint, create a login route:

-   POST '/login' : passing in email and password, validated by login_schema
-   After credentials have been validate utilizes the encode_token() function to make a token to be returned to that customer.

Create @token_required wrapper, that validates and unpacks the token, and stores the id in the request as a field. Create a route that requires a token, that returns the service_tickets related to that mechanic.

-   GET '/my-tickets': requires a Bearer Token authorization. **(OPTIONAL... for now will be required in the end project)**
-   The route function should extract the mechanic_id from the request.
-   Using that id query the service_tickets that belong to the mechanic.

Additionally add @token_required to any routes you think should require authorization. (ex: Update, Delete,...)