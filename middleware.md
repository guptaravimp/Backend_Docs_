# Writing middleware for use in Express apps
## Overview

Middleware functions are functions that have access to the request object (req), the response object (res), and the next function in the application’s request-response cycle. The next function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.


Middleware functions can perform the following tasks:


1. Execute any code.
2. middleware are used to do validation , authentication , authorization and etc 

3. Make changes to the request and the response objects.

4 End the request-response cycle.

5 Call the next middleware in the stack.
