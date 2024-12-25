![image](https://github.com/user-attachments/assets/9c63a251-225f-43b0-b70c-6d608454ad41)# Now we are going to do work on MongoDB Atlas that  is cloud based database 
### Now we not store our data in local host our system we are going to use the Mongodb Atlas that is cloud based database service provided by Mongodb 
# 1-> Go and Link 
https://cloud.mongodb.com/v2/676c4dba74ee353776c6b61c#/overview

## Login with Your emailID and password email is- tectravibusiness@gmail.com
## You see the screen 
![Screenshot 2024-12-26 001015](https://github.com/user-attachments/assets/1b10b4bb-89e5-4a8f-a0d2-23fc5bcc3b1f)

# 2-> Now lets connect it to do work 
## click on connect
## Looks like this 
![Screenshot 2024-12-26 001236](https://github.com/user-attachments/assets/7ba71b6f-ebb7-42c6-aab2-5dcdfd83023c)

## Now we select compass
## Looks like this 
![Screenshot 2024-12-26 001411](https://github.com/user-attachments/assets/c6814787-fa44-475d-ab67-0f4057cf6a8b)

# 3-> Copy the connection string 
```
mongodb+srv://techravibusiness:<db_password>@clusterone.t9ol1.mongodb.net/
```
## use password in place of (db_password) and 
## Now click on done

![Screenshot 2024-12-26 001638](https://github.com/user-attachments/assets/1897a45f-f18e-4e54-97e0-e09f2eb949b6)

# 4-> Now go to your local MongoDB Compass 
## create connection using the connection string with password replaced 
```
mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/
```
## Look like this 

![Screenshot 2024-12-26 001940](https://github.com/user-attachments/assets/6aba7f81-62b8-41d5-a0c1-9b8e9dda597d)

# 5-> Now save and connect 
## Now You can see my Cloud based database is connected to my Mongodb compass now we can create database , update database document etc we can do any task and perform operation 
## that will automatticly refelected in our cloud based database 

![Screenshot 2024-12-26 002155](https://github.com/user-attachments/assets/289671e5-1194-45ed-b20c-154a19f94227)

# 6-> Now let create our Own Database 
## Click on + icon on our connection 

![Screenshot 2024-12-26 002451](https://github.com/user-attachments/assets/d900277b-52f6-4c9a-a9db-60f19ef0a9c0)

## and create a item Named Database and cars named collection 

![Screenshot 2024-12-26 002800](https://github.com/user-attachments/assets/2d8c439e-4e1f-4384-9040-31f2de7df672)   

# click on create database 
## Looks like this 

![image](https://github.com/user-attachments/assets/39187b22-bf91-421e-a49a-34ef6b1cc73b)

# 7-> Now let insert Document inside this databsae

```
{
  "_id": {
    "$oid": "676c56fe04a711218546c673"
  },
  "name":"Scorpio",
  "Price":2500000
}
```
## Like this 

![Screenshot 2024-12-26 003521](https://github.com/user-attachments/assets/1e2f2e3c-03a7-4050-83fb-ce919015af16)

# 8-> click on insert and see 
## the data are inserted in our Mongodb compass 
## IMP-> Actually this data is also added in our cloud mongodb atlas because we connected that server that connectection 

# 9-> go to mongodb atlas and click on browse collections 

![Screenshot 2024-12-26 004545](https://github.com/user-attachments/assets/80625f42-decb-485a-9eaf-49b0776cdc7d)

## see the item and car collection also added in our cloud database 

![Screenshot 2024-12-26 004647](https://github.com/user-attachments/assets/43a32ccf-6115-4dc8-90c0-7ae701fe463c)

## and see inserted document is also present here 

# IMPPPP_____ 10 - Now we can see our all database inside vs code also 
## Go to vs code and search extension (Mongodb for vs code) and install this 

![Screenshot 2024-12-26 005333](https://github.com/user-attachments/assets/b688f7b0-7b73-48fc-9e91-a1e046170149)

## Now click Mongodb icon on left side below env

![Screenshot 2024-12-26 005442](https://github.com/user-attachments/assets/9779b36c-b840-47ba-98cb-22374407f8e1)

##  after clicking looks like this 

![Screenshot 2024-12-26 005643](https://github.com/user-attachments/assets/4a18c6ad-07f8-4c7f-9c48-32b6c48b315a)

# 11-> Now click on connect 
## and paste Your connection string that You replace with your password i.e
```
mongodb+srv://techravibusiness:0GstLwwIVhqIVOe1@clusterone.t9ol1.mongodb.net/
```
## Now looks like this 
![image](https://github.com/user-attachments/assets/f9fa11da-cfa2-4fad-89a4-6025043210a9)

# 12-> press enter and You can see Your all database on this server
## here You can also update delete and do all operation etc 








