
# Creating a e-commerce backend product application 
## first setup and connect mongodb using 
### https://github.com/guptaravimp/Backend_Docs_/blob/main/connectMongoose.md

# 1. Now let we want give our database name in place of test named database 
## add the database name at the dn of connection string like this 
```
MONGODB_URI=mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/
```
## TO
```
MONGODB_URI=mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/ecommerceDB
```

# 2. Now lets add our port in .env file also 
## go to .env file write 
```
PORT=3000
```
## Now import this in index.js where we use this port 
```
const dotenv=require('dotenv')

// load env config 
dotenv.config();
const port = process.env.PORT
```
# 3. Create a models 
## create a models folder inside backend project and create a file names as  (productModel.js)
## write the model and schema of the product model 

```

const {
    Schema,
    model
  } = require("mongoose");
  

  const ProductSchema = new Schema({
    name: {
      type: String,
      required: true,
      maxlength: 50
    },
    price: {
        type: Number,
        required: true,
    },
      description: {
        type: string,
        required: true,
    },
      category: {
        type: string,
        required: true,
    },
    
    createdAt: {
      type: Date,
      default: Date.now,
    },
  });
    // database json name product
  const ProductModel = model("product", ProductSchema)

module.exports = ProductModel
```
# 4. Now let crearte a folder inside the backend project named as ( controller )for the logics

## see the project structure 
## In controllers file we write all the business logic 

![Screenshot 2024-12-29 121510](https://github.com/user-attachments/assets/787a1c84-965a-4d54-8101-9dc7db81f279)

## create file named productController.js inside this controllers flder 
## and write the below code inside this file 

```
const Product=require('../models/productModel')


// business logic
const getProduct=async(req,res)=>{
    try{
        // fetching all the products from product db collections 
        const allProduct=Product.find();
        if(!allProduct){
            res.json({
                message:"There is no product"
            })
        }
        // if we have product greate than  1 
        res.status(200).json({
            success:true,
            products:allProduct,
        })
      
    }
    catch(err){
     res.status(500).json({
        success:false,
        message:"Internal server error "
     })
    }
}
```
# 5-> Now create a routes folder and routes file we want to access these data 
## create folder anmed as routes and create a file name inside anmed as (productRoutes.js)

```
const express = require('express');
const router = express.Router();
const {getProduct}=require('../controllers/productController')
// CRUD Operations

// View/Read
// frontend se call aai ek get request for this path 
// get request hit hui and kaha es controller pr chale jao 
// aur yr dekhoge controller to ye ssare product ko res me send kiya hai 
router.get('/products',getProduct );


// Create


module.exports = router;

```

# 6. Now import this mount this isnside index.js file 
```
const productroute=require('./routes/productRoutes')
app.use('api',productroute)
/// -> /api/products

```



