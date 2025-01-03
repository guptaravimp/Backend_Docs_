# Writing middleware for use in Express apps
## Overview
use documentation : https://expressjs.com/en/guide/writing-middleware.html
Middleware functions are functions that have access to the request object (req), the response object (res), and the next function in the application’s request-response cycle. The next function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.


Middleware functions can perform the following tasks:


1. Execute any code.
2. middleware are used to do validation , authentication , authorization and etc 

3. Make changes to the request and the response objects.

4 End the request-response cycle.

5 Call the next middleware in the stack.
# 1. No first setup backend project using below documentation 
### https://github.com/guptaravimp/Backend_Docs_/blob/main/Setup_Into.md
# 2 Now we are going to write middleware 
## 1- inbuilt middleware 
### (i)-> express.json() 
it is used when we are dealing with json onject 
it is used to convert this json into valid javascript object to use in our web application 
like this 
```
// middleware inbuild express.json use to convert json data in valid hjavascript object
app.use(express.json())

app.get('/', (req, res) => {
  console.log(req.body);
  console.log("hello ")
  res.send('Hello World!')
})

```
## Now let send the body data from postman 
![Screenshot 2024-12-23 145355](https://github.com/user-attachments/assets/495df674-e973-4f58-b8cc-98390db9d704)
## Now go to console you can see the valid javascript data will consoled below 
## 2 -> lets create our own  iddle ware of logging 
req->logging->Authentation->validation->response 
```

const express = require('express')
const app = express()
const port = 3000


/// sue middleware inbuild express.json use to convert json data in valid hjavascript object 

app.use(express.json())
/////middleware of logging , validation , authentation
// req->logging->auth->validation->res  
/// creating a middleware 
const loggingMiddleware=function (req,res,next){
    console.log("Loging kar raha hu ");
    next();
}
/// loading middleware into a application 
app.use(loggingMiddleware); //loading our middleware

const auth=function (req,res,next){
    console.log("authentation ho gaya ")
    next();
}
app.use(auth);

const validation =function (req,res,next){
    console.log("validation ho gaya ")
    next();
}
app.use(validation);

app.get('/', (req, res) => {
  console.log("Mai route Handler hu ")
  console.log(req.body);  // that is calling body req that is in postman 
  res.send('Hello World!')
})


app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
})
```
## Again send data from postman like this 
![Screenshot 2024-12-23 145355](https://github.com/user-attachments/assets/495df674-e973-4f58-b8cc-98390db9d704)

Now You can see the console --------

![Screenshot 2024-12-23 151017](https://github.com/user-attachments/assets/f2205821-d4fc-454d-a513-3957758ad6ef)


# Now let using middle ware 
see documentation    :    https://expressjs.com/en/guide/using-middleware.html




