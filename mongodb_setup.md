
# Tutorial TO setup MongoDB Database in Our Backend Project 
## Download MongDB Community Server using link
### https://www.mongodb.com/try/download/community
## Download MongoDB Campass using below link :
### https://www.mongodb.com/try/download/compass

# After Installation our DB campass Lokks like this 
![Screenshot 2024-12-25 232514](https://github.com/user-attachments/assets/22cdc6be-4ff6-4cda-86c1-8873ef9d1971)

# 1-> Now lets create connection click on add new connection and create connection
![Screenshot 2024-12-25 232712](https://github.com/user-attachments/assets/c758c49c-f10e-4ce0-b132-7d6f56383b26)

# 2-> After creation is look like this 
![Screenshot 2024-12-25 232753](https://github.com/user-attachments/assets/e973932a-7998-41e6-be7b-4036ca680278)

## Now see the 3 Database are present (admin,config,local) 
# 3-> Now lets create a collections in local Click on Local see this 

![Screenshot 2024-12-25 233003](https://github.com/user-attachments/assets/542caec1-819b-49e1-845c-deb2f58326c7)

# 4-> click on create collection and create the collection like this 
![Screenshot 2024-12-25 233115](https://github.com/user-attachments/assets/ae399cbf-2bf5-4860-8279-3ca4f3ac0c57)

# 5-> Now lets create or insert or delete or update the document objects 
## click on adddata-> insertocument 
![Screenshot 2024-12-25 233233](https://github.com/user-attachments/assets/6d126a0d-6994-40f5-96db-43372889f206)

# 6-> let insert saome data 
```
{
  "_id": {
    "$oid": "676c48f077a930793a582d13"
  },
  "name":"RAVI GUPTA",
  "ROll_No":23132,
  "college":"RIC basti"
}
```

![Screenshot 2024-12-25 233419](https://github.com/user-attachments/assets/97b672b9-da5c-45be-9632-5028d51be07e)




# 6-> cick on insert and looks like thuis 

![Screenshot 2024-12-25 233552](https://github.com/user-attachments/assets/cf35d329-6a19-4638-8019-57dc684a51e0)

# 7-> Now here we can update delete and do more operation here 
## and we can add more data here 
![Screenshot 2024-12-25 233804](https://github.com/user-attachments/assets/e32e0cee-5d85-4b85-a0ab-4a6bba5934bb)

# 8-> Now to show all the data we can use open mongodb shell  see all the data
## RUn the command in shell
```
db["Users"].find()
```
## You can see 
![Screenshot 2024-12-25 233921](https://github.com/user-attachments/assets/e81c7b98-2723-485d-8344-c5fa6cd5b891)



