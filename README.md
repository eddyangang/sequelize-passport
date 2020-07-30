# Sequelize and Passport Example 

### With detailed explanation. 

* * * 
<strong>Config</strong>

<u>Middleware</u>

isAuthenticated 
```
Exports a middleware function that checks if a user is a member. If a valid user, then move on to the next middleware function; else redirect to the home page. 
```
Config.json
```
Configuration for database for depending on which stage of production (test, development, production)
```
Passport.js
```
A library used to authenticate a user based on email and password credentials. The variable passport uses a  “middleware” like function to determine whether a user has entered a valid email and password. If either the email or password is incorrect, it will return false with a message indicating which is incorrect. If correct, the function will return the user as an argument. SerializeUser will save the user id to the session file in the browser as a cookie and add the user object to the request object as a req.user. Deserializeuser will return the user’s cookie so that authentication is not required the next time the user tries to login from the same browser. 
```
* * * 
<strong>Models</strong>

Index.js
```
A boilerplate template made by Sequelize to iterate each file in the “models” folder to define tables in our database. In this case, we are only worried about creating a table to store the user’s information. 
```
User.js
```
Exports a constructor function that will define a user with an email and password. The “validpassword” method will compare the user’s submitted password with the encrypted password saved in the database and return true if it matches, and false otherwise. The “addhook” method will hash the users password before the user is created and saved into the database. 
```
* * *

<strong>Public</strong>

<u>JS</u>

Login.js
```
When the document is fully loaded, it will listen for the submit button and get the user’s email and password input. A ajax post request is then made sending this information to the login API route where the credentials will be checked to determine whether the user will move on to the /members page or an error will show otherwise. The form fields are then cleared. 
```
Stylesheets
```
Styling is made here
```

Login.html
```
The login page where the email and password input is collected from the user and the information will ultimately be sent to the /api/login route to determine validity. 
```
Members.html
```
The members page when the user enters after a successful login
```
signup.html
```
The sign up page where the user can sign up for the first time. Information is ultimately sent to the /api/signup route in api-routes file.
```
* * *

<strong>Routes</strong>

Api-routes.js
```
This folder contains middleware functions to manipulate the request and response before reaching either the server or client. The app.post function will take in the login information made by the user and passes it to the passport module mentioned earlier. The passport has a method called “authenticate” which will determine if the credentials submitted are valid. If valid, the user will be sent to the members page. Otherwise an error will be sent. 

/api/signup will add the users signup information into the database and redirect them to the login page where they can now login with their new account. 

“/logout” will logout the user and redirect them back to the root page. 

“/api.user_data” will send back the email and id of a logged in user. Will send back an empty object if signed out. 
```
Html-routes.js
```
app.get(“/”... will direct the member to the members page if the user is already logged in. Otherwise it will send the user to the signup page. 

app.get(“/login”... will send the user to the login page if the user is already signed in. Otherwise will send the user to the login page/ 

app.get(“/members”... takes in a middleware callback function called “isAuthenticated” to check if the req accessing the /members page is a valid user. If valid, move on to the next middleware function. Since there is only one middleware function for this route, it will send the user to the members.html page . Else it will indirectly send the user to the signup.html page.
```
Package.json
```
A json package that lists all of our dependencies used in this project. 
```
Server.js
```
Creates our express application which uses all of the /api/routes made in our api-routes.js file. It syncs with our database if it exists or creates the database otherwise before the server is made listening on the port. 
```





