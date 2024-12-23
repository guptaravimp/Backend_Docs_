# Writing middleware for use in Express apps
## Overview

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

