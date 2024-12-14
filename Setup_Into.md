# Backend Project Setup Documentation
## Prerequisites
1-> Ensure the following tools are installed:

(i)  Node.js (Download from nodejs.org)

(ii) MySQL Database (Install MySQL server and a GUI like MySQL Workbench)

(iii) npm (Comes with Node.js)
# 1. Initialize the Project
## Create a new directory for your project:
```
mkdir backend-project
cd backend-project
```
# 2. Initialize a new Node.js project:(in terminal Inside backend_project folder name )
```
npm init -y
```
# 3- Create Index.js or say Server.js file to write our backend code 
## entry point: (index.js)

# 4- Install expree
```
$ npm install express
```
# Now write this code in server.js 
```
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
# 5 Now run this backend in Node.js
```
node server.js
```
see the port ......
