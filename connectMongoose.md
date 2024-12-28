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
# Now let create Routes folder to perform CRUD operation 
## first create a routes folder inside backend project 
## inside this let create a file named as (app.js)
## Now to perorm these operations first import the (UserModel.js)
## import express and router also
```
const express=require('express')
const router=express.Router();
const User=require('../models/userModel')
```
## Now let first we fetch the and read the all user present in (Usermodel.js)

```
const express=require('express')
const router=express.Router();
const User=require('../models/userModel')


// routes


// Crud Operations


//view/Read
router.get('/user',async(req,res)=>{
         try{
            // fetching all the data of user in User 
            const users=await User.find();
            res.status(200).json(users);
         }
         catch(err){
            res.status(500).json({
                success:false,
                message:err.message
            })
         }
})
```


