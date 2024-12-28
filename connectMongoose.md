#  This tutorial will help to connect node js with mongodb using mongoose 
## means server-> Database ko communicate karne ke liye jiska use karte hai uska naam hai mongoose 
## Great article on this ->
https://www.topcoder.com/thrive/articles/how-to-connect-mongodb-to-node-js-using-mongoose
# 1 -> First setup backend using 
https://github.com/guptaravimp/Backend_Docs_/blob/main/Setup_Into.md
## Now install some more package :
```
npm i mongoose
npm i dotenv
```
# 2-> create a db.js folder inside the project like index.js 
## write this code to connect with mongodb 
### Importing
```
const mongoose = require('mongoose');
```
### connection code 
#### in place of url use your connection string od mongodb 
connection string : ```mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/```
```
const connectDB = async () => {
    try {
      const conn = await mongoose.connect(`mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/`, {
        useNewUrlParser: true,
      });
      console.log(`MongoDB Connected`);
    } catch (error) {
      console.error(error.message);
      process.exit(1);
    }
  }
  module.exports = connectDB;
```
# 3-> Now let we want to use this db in any file like :
## let import in index.js to use this 
```
const connectDB = require('./db');
```
## let connectdb
```
//connect to database
connectDB();
```
## use bodyparser to parse the data 
```
//body parser
app.use(express.json());
```
# 4- Now see the terminal database is connected now 

![Screenshot 2024-12-28 123019](https://github.com/user-attachments/assets/37beeb6e-18cd-424e-8a9f-fecb048382f3)

# 5-> Now to secure our data with .env file
## to secure our some confidential data and information like api key , some password we use .env file inside our backend project 
## create a file name .env
#### let we secure our connection string inside .env
```
MONGODB_URI=mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/
```
## Now go to file where you use this url and change it to \
## here db.js file
### replace url with
```
process.env.MONGODB_URI
```
## and import it and load dotenv config like this 
```
const dotenv=require('dotenv')

// load env config 
dotenv.config();
```
## Now your data is secure 
## Now you db.js looks like this 
```
const mongoose = require('mongoose');
const dotenv=require('dotenv')

// load env config 
dotenv.config();

const connectDB = async () => {
    try {
      const conn = await mongoose.connect(process.env.MONGODB_URI, {
        useNewUrlParser: true,
      });
      console.log(`MongoDB Connected`);
    } catch (error) {
      console.error(error.message);
      process.exit(1);
    }
  }
  module.exports = connectDB;
```

# 6-> Now lets create a models and schema to perform crud operation
## first create a folder name as (models) and 
### inside this create a file name as let (UserModel.js)
### Import and define this inside Usermodel.js
```
const {
  Schema,
  model
} = require("mongoose");

```
## Now let create a schema inside the model file named Usermodel.js

```
const UserSchema = new Schema({
    name: {
      type: String,
      required: true,
      maxlength: 50
    },
    age:{
        type:Number,
        required:true
    },
    weight:{
        type:Number
    },
    createdAt: {
      type: Date,
      default: Date.now,
    },
  });
```

## Now export this model
```
const UserModel = model("test", UserSchema)

module.exports = UserModel
```
## See this complete code of Usermodel.js
```
const {
    Schema,
    model
  } = require("mongoose");


const UserSchema = new Schema({
    name: {
      type: String,
      required: true,
      maxlength: 50
    },
    age:{
        type:Number,
        required:true
    },
    weight:{
        type:Number
    },
    createdAt: {
      type: Date,
      default: Date.now,
    },
  });

const UserModel = model("test", UserSchema)

module.exports = UserModel
```
# 7-> Now let create Routes folder to perform CRUD operation 
## first create a routes folder inside backend project 
## inside this let create a file named as (users.js)
## Now to perorm these operations first import the (UserModel.js)
## import express and router also
```
const express=require('express')
const router=express.Router();
const User=require('../models/userModel')
```
## Now let first we fetch the and read the all user present in (Usermodel.js)

```
const express = require('express');
const router = express.Router();
const User = require('../models/userModel');

// CRUD Operations

// View/Read
router.get('/user', async (req, res) => {
    try {
        // Fetching all user data
        const users = await User.find();
        res.status(200).json(users);
    } catch (err) {
        res.status(500).json({
            success: false,
            message: err.message,
        });
    }
});

// Create
router.post('/user', async (req, res) => {
    try {
        const { name, age, weight } = req.body;
        // Creating a new user instance
        const newUser = new User({ name, age, weight });
        // Saving the instance to the database
        await newUser.save();
        res.status(201).json({
            success: true,
            message: 'User created successfully',
            data: newUser,
        });
    } catch (err) {
        res.status(500).json({
            success: false,
            message: err.message,
        });
    }
});

module.exports = router;

```
# 8-> Now let import router folder inside index.js
```
const user=require('./routes/users')
app.use('api',user)
```

# 9-> now let post some data using postman 
#  9.1-> Post method
## go to postman and check api post mehtod request
```
http://localhost:3000/api/user
```
## Now see this data is successfully post 

![Screenshot 2024-12-28 154728](https://github.com/user-attachments/assets/95f907a7-a8f4-4d4c-a767-7ec46c543233)

## Now go to mongodb compass or mongodb atlas and you can see the data is also inserted into DB 
## see this 
## test named db is created and data is pushed into it 

![Screenshot 2024-12-28 155300](https://github.com/user-attachments/assets/fee786d9-f2bf-44f0-81ed-e465862466ec)

# 9.2-> see the get request also on this url-> http://localhost:3000/api/user  on postman 

![Screenshot 2024-12-28 155425](https://github.com/user-attachments/assets/ccd362c8-b4a3-4831-aa06-a6ef63665ace)

# 9.3 Now let update some detail using put method 
## go to routes folder inside this go to (users.js) and add the put mehtod code 
```
const express = require('express');
const router = express.Router();
const User = require('../models/userModel');

// CRUD Operations

// View/Read
router.get('/user', async (req, res) => {
    try {
        // Fetching all user data
        const users = await User.find();
        res.status(200).json(users);
    } catch (err) {
        res.status(500).json({
            success: false,
            message: err.message,
        });
    }
});

// Create
router.post('/user', async (req, res) => {
    try {
        const { name, age, weight } = req.body;
        // Creating a new user instance
        const newUser = new User({ name, age, weight });
        // Saving the instance to the database
        await newUser.save();
        res.status(201).json({
            success: true,
            message: 'User created successfully',
            data: newUser,
        });
    } catch (err) {
        res.status(500).json({
            success: false,
            message: err.message,
        });
    }
});
// update
router.put('/user/:id',async(req,res)=>{
    const {id}=re.params;
    const {name,age,weight}=req.body;
    try{
                 const updatedUser=User.findByIdAndUpdate(id,{name,age,weight})
                 if(!updatedUser){
                    res.json({
                        messgae:"User Not Found"
                    })
                 }
                 // but if updayed user successfully
                 res.status(200).json({
                    success:true,
                    user:updatedUser
                 })
    }catch (err) {
        res.status(500).json({
            success: false,
            message: err.message,
        });
    }
})

module.exports = router;

```
## Now let update the data of ravi Gupta and with the id (676fd08894c5b514241aceab)
### so create the routes -> http://localhost:3000/api/user/676fd08894c5b514241aceab/
## Now hit send in postman see this 

![Screenshot 2024-12-28 161118](https://github.com/user-attachments/assets/4a009d1e-3951-4eff-aa1f-b4ba3edd3175)

## Now go to atlas database and see that the ravi gupta is updated to akshat
## see this 

![Screenshot 2024-12-28 161309](https://github.com/user-attachments/assets/04dfefbb-cc3f-4b62-b9e2-c1eb511fe418)




