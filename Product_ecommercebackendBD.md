
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

