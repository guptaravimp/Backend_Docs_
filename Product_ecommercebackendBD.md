
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

/// updating product detail 
router.put('/products/:id',updatedProduct );
```

# 13. Now let update the data of brush from postman 

![Screenshot 2024-12-29 132727](https://github.com/user-attachments/assets/56336397-e84a-4dfa-a1a0-e05200e40a1d)

## You can see that data is succesfully updated 

![Screenshot 2024-12-29 183842](https://github.com/user-attachments/assets/e5d577a9-6bc8-4c0d-afa5-804138ecc6f9)

## See this get method 
![Screenshot 2024-12-29 184118](https://github.com/user-attachments/assets/aa637a6c-28b6-4dbf-997f-ff5b66a24c87)

# 14 Now same as if we run logic of createProduct controller
## Go to productRoutes.js and add the login and import the creatproduct also 
```
const {getProducts, updatedProduct, createProduct}=require('../controllers/productController')

/// create new product detail 
router.post('/products',createProduct );
```
## see this is successfully added and created new productas 

![Screenshot 2024-12-29 184915](https://github.com/user-attachments/assets/ad823021-c00b-4bc4-a514-1dca7db69181)


# 15 . Now lets implement the logic of delete method `
## Now add the logic of delete inside the (productController.js)
```
const deleteProduct=async (req,res)=>{
    try{
        const {id}=req.params;
        const deletedProduct=await Product.findByIdAndDelete(id)

        if(!deletedProduct){
            res.json({
                message:"product not found"
            })
        }

        res.status(200).json({
             success:true,
             Product:deletedProduct,
             message:"deleted succesfully "
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
## Now export it also see the conplete code of productController.js 
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
const updatedProduct=async (req,res)=>{
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

/// delete product
const deletedProduct=async (req,res)=>{
    try{
        const {id}=req.params;
        const deletedProduct=await Product.findByIdAndDelete(id)

        if(!deletedProduct){
            res.json({
                message:"product not found"
            })
        }

        res.status(200).json({
             success:true,
             Product:deletedProduct,
             message:"deleted succesfully "
        })
    }
    catch(err){
        res.status(500).json({
            success:false,
           message:"Internal server error "
        })
       }
}
module.exports={getProducts,createProduct, updatedProduct, deletedProduct}
```
## Now lets lets import this inside the product routes to create a route of delete product 
## go to (productRoutes.js)

```
const {getProducts, updatedProduct, createProduct, deletedProduct}=require('../controllers/productController')
router.delete('/product/:id',deletedProduct)
```

# 16. Now go to postman and hit the request of delete
## for some specific id lets for brush3

![Screenshot 2024-12-29 191300](https://github.com/user-attachments/assets/ae0e3489-796e-488b-aad5-5c88cc0d7402)

## see this now only 2 reamining 

![image](https://github.com/user-attachments/assets/f2d96338-db60-4bf8-8668-55344e820676)








