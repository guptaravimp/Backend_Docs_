# Routing
refers to how an application’s endpoints (URIs) respond to client requests. For an introduction to routing, see Basic routing.

You define routing using methods of the Express app object that correspond to HTTP methods; for example, app.get() to handle GET requests and app.post to handle POST requests. For a full list, see app.METHOD. You can also use app.all() to handle all HTTP methods and app.use() to specify middleware as the callback function (See Using middleware for details).

Documentation : https://expressjs.com/en/guide/routing.html
# Now let first setup the backend project 
 See Documentation : https://github.com/guptaravimp/Backend_Docs_/blob/main/Setup_Into.md

 # 1-> Now go to the index.js or server.js 
 ## lets us write the all get, post,put, delete method and do testing using postman 
 write this code inside server.js or index.js 
 
 ```
const express = require('express')
const app = express()
const port = 3000

// app.get('/', (req, res) => {
//   res.send('Hello World!')
// })
// request ki kahani 
// get request 
app.get('/',(req,res)=>{
 res.send("Got a Get request");
})
app.post('/items',(req,res)=>{
    res.send("got a post request");
})
app.put('/item/:id',(req,res)=>{
    res.send("Got a put request");
})
app.delete('/item/:id',(req,res)=>{
    res.send("Got a delete request");
})
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
## Now go to postman and create a workspace and create a colletction and check all rotes are working properly 
to use postman see the documentation : 
# 2 Now let use another mehtod i.e app.sendFile() method
first create a html file named as (index.html) inside folder and write some frontend code in html that we want to send on that server 
### Now go to server.js and update the code inside get method 
```
app.get('/',(req,res)=>{
// res.send("Got a Get request");
res.sendFile('./dummy.html',{root:__dirname})
})
```
### Now go to postman and send the request of http://localhost:3000/ using Get method
### Now you can see the reponse is the complete code of html and you can preview it 
![Screenshot 2024-12-14 175427](https://github.com/user-attachments/assets/7faac63c-2d94-4cfa-ae38-46c2526c750e)

# Now after this let if we createad a big project then we have to face a diffficulty of index.js to store all routes and send response so we use Routes folder in which all routes of all types like blogs routes , course routes etc can be store so go to project folder and create a routes folder 
![Screenshot 2024-12-22 193923](https://github.com/user-attachments/assets/9d950e19-52db-4d45-99bc-d93f304bf578)
## Now create a routes files let create a route file item.js
![Screenshot 2024-12-22 195336](https://github.com/user-attachments/assets/84f794ab-6bc3-4a18-9ebf-c6fe2b58e2e8)
## now write all the routes of get, post, update, delete into it and iniltialize this file like this given below
```
//ye file saare item spwcific routes ko store karegi 

const express = require('express')
const router = express.Router()

// define the home page route
router.get('/',(req,res)=>{
    res.send("Got a Get request");
    // res.sendFile('./dummy.html',{root:__dirname})
})
router.post('/items',(req,res)=>{
        res.json({"1":23,"z":32});
})
router.put('/item/:id',(req,res)=>{
        res.send("Got a put request");
})
router.delete('/item/:id',(req,res)=>{
        res.send("Got a delete request");
 })
 //->/api/-> item homepage 
 //-> /api/items ->item post request
 //-> /api/items/id ->put/delete request

module.exports = router
```

## Now to use this item.js all routes go to the index.js file and import and use like below-> inside index.js 
```
const item=require('./routes/item')
app.use('/api',item)
```
full code of index.js
```

const express = require('express')
const app = express()
const port = 3000
const item=require('./routes/item')
 
app.use('/api',item)


app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
# Now go to postman and test these routes like 
## http://localhost:3000/api/                 ->  fo homepage

## http://localhost:3000/api/item                 ->  fo item
## etc

 
