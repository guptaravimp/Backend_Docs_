
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
# 7. Now go to Mongodb atlas or Mongodb compass beacuse we connected previously our mongodb atlas to mongodb compass 
## Now see that ecommerceDB named database is created and product collection is also created 

![Screenshot 2024-12-29 123842](https://github.com/user-attachments/assets/2bbc91a0-aa9a-41d1-84a0-a1f2b70e4d2b)

# 8. Now go to the Postman and check the routes of product

```
http://localhost:3000/api/products
```
## as yet it is empty so ypu can see this 

![Screenshot 2024-12-29 124506](https://github.com/user-attachments/assets/ff4f1c9d-00a9-4994-b89e-be4d4e93ab87)

## but something error beause it should have to returer
## there is no products so add the logic that when it is empty also tghen should returen there is no producst 
## inside controller file 
 ```
if(!allProduct || allProduct.length===0){
            res.json({
                message:"There is no product"
            })
        }
```
##   Now see the corrected outcome on postman 

![Screenshot 2024-12-29 124844](https://github.com/user-attachments/assets/ce184d91-a03b-4d7f-a8e8-059581599897)


# 9. Now let insert some data into this database from mongodb atlas or compass 
## brush and chappal see this 


![Screenshot 2024-12-29 125645](https://github.com/user-attachments/assets/f5b14189-815a-42ca-b5f2-fbfca25b34b3)

# 10. Now you can see the get request in postman see all the data 

![Screenshot 2024-12-29 125813](https://github.com/user-attachments/assets/5c21150f-a9ee-4e04-8aa0-3d88631b4798)

# 11. Now lets implement the logic of (create, update and delete) method in our controller file 

```
/// create product logic 
const createProduct=async (req,res)=>{
    try{
         const {name,price,description,category}=req.body
         const newProduct=new Product({name,price,description,category});
         await newProduct.save();
         res.status(200).json({
            success:true,
            product:newProduct

         })
    }
    catch(err){
        res.status(500).json({
           success:false,
           message:"Internal server error "
        })
       }
}


// update controller 
const updateProduct=async (req,res)=>{
    try{
        const {id}=req.params;
        // kuyuki abhi ham body se hi data ko bhej rahe hai baa me apne admin se lekar add kar denge 
        const {name,price, description,category}=req.body;
        const updatedproduct=await Product.findByIdAndUpdate(id,{name,price,description,category},{new:true})
        res.status(200).json({
            product:updatedproduct
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

## complete filr looks like this named is (productController.js)

```
const Product=require('../models/productModel')


// business logic
const getProducts=async(req,res)=>{
    try{
        // fetching all the products from product db collections 
        const allProduct=await Product.find();
        if(!allProduct || allProduct.length===0){
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




/// create product logic 
const createProduct=async (req,res)=>{
    try{
         const {name,price,description,category}=req.body
         const newProduct=new Product({name,price,description,category});
         await newProduct.save();
         res.status(200).json({
            success:true,
            product:newProduct

         })
    }
    catch(err){
        res.status(500).json({
           success:false,
           message:"Internal server error "
        })
       }
}


// update controller 
const updateProduct=async (req,res)=>{
    try{
        const {id}=req.params;
        // kuyuki abhi ham body se hi data ko bhej rahe hai baa me apne admin se lekar add kar denge 
        const {name,price, description,category}=req.body;
        const updatedproduct=await Product.findByIdAndUpdate(id,{name,price,description,category},{new:true})
        res.status(200).json({
            product:updatedproduct
        })

    }
    catch(err){
        res.status(500).json({
           success:false,
           message:"Internal server error "
        })
       }
}
module.exports={getProducts,createProduct, updatedProduct}
```
# 12. Now add this routes in route file 
## first import this in productRoutes.js file 

```
const {getProducts, updatedProduct, createProduct}=require('../controllers/productController')
/// creating product
router.put('/products/:id',createProduct );
/// updating product detail 
router.update('/products/:id',updatedProduct );
```





