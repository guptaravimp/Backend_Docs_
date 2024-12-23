
# Routes specific middle ware 
## that is used like logging authentication that isstudent or admin for our websites 
## req->authentication->(isstudent->response)or (isadmin->response)
# 1- let first setup our project using below docs :
https://github.com/guptaravimp/Backend_Docs_/blob/main/Setup_Into.md
# Now create a routes folder because we want to write our code in rout file rather than writing in index 
## routes folder->route.js file 
## Now lets creat authentication middleware, isstudent middleware, isadmin middleware 

```
/// middleware creation 
// Middleware
router.use(express.json());

const auth = function (req, res, next) {
    console.log("I am inside auth middleware");
    // Dummy user added for testing
    req.user = { userId: 1, role: "Student" };
    if (req.user) {
        next();
    } else {
        res.json({
            success: false,
            message: "Not a valid user"
        });
    }
};

const isStudent = function (req, res, next) {
    console.log("I am inside student middleware");
    if (req.user.role === 'Student') {
        next();
    } else {
        res.json({
            success: false,
            message: "Access denied, this route is only for students"
        });
    }
};

const isAdmin = function (req, res, next) {
    console.log("I am inside admin middleware");
    if (req.user.role === 'admin') {
        next();
    } else {
        res.json({
            success: false,
            message: "Access denied, this route is only for admins"
        });
    }
};
```
## No create our routes inside this 
```
/// routes
router.get('/Student',auth,isStudent,(req,res)=>{
    console.log(" I am inside student router")
    res.send("Got a student  request");
})
router.get('/admin',auth,isAdmin,(req,res)=>{
    console.log("I am  inside admin routes")
    res.send("Got a admin request");
})
```
## now complete code of route.js is 
```
//ye file saare item specific routes ko store karegi 

const express = require('express');
const router = express.Router();

// Middleware
router.use(express.json());

const auth = function (req, res, next) {
    console.log("I am inside auth middleware");
    // Dummy user added for testing
    req.user = { userId: 1, role: "Student" };
    if (req.user) {
        next();
    } else {
        res.json({
            success: false,
            message: "Not a valid user"
        });
    }
};

const isStudent = function (req, res, next) {
    console.log("I am inside student middleware");
    if (req.user.role === 'Student') {
        next();
    } else {
        res.json({
            success: false,
            message: "Access denied, this route is only for students"
        });
    }
};

const isAdmin = function (req, res, next) {
    console.log("I am inside admin middleware");
    if (req.user.role === 'admin') {
        next();
    } else {
        res.json({
            success: false,
            message: "Access denied, this route is only for admins"
        });
    }
};

// Routes
router.get('/student', auth, isStudent, (req, res) => {
    console.log("I am inside student route");
    res.send("Got a student request");
});

router.get('/admin', auth, isAdmin, (req, res) => {
    console.log("I am inside admin route");
    res.send("Got an admin request");
});

module.exports = router;

```
# 2- Now let linked or mounting our routes with index.js 
```
const route=require('./routes/route')
//  Mounting the route 
app.use('/api',route)
```
## complete code of index.js
```
const express = require('express')
const app = express()
const port = 3000

const route=require('./routes/route')
//  Mounting the route 
app.use('/api',route)

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
# Now testing using postman go and use getmethod 
```
http://localhost:3000/api/student
```
You will see response that -> Got a student  request   because the student is valid 
```
http://localhost:3000/api/admin
```
You will see -> 
````
{
            success:false,
            message:"Not a valid user "
}
````

