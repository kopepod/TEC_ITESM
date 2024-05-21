# MongoDB Tutorial

Contents:
1. Install
2. Create database
3. Simple Query
4. Call from Django

## 1. Install

```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc |    sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg    --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
cat /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
sudo systemctl status mongod
```
(Optional install compass) https://www.mongodb.com/try/download/compass

## 2. Create databse

```bash
echo -e "Name,Email,Age\nJohn Doe,jonhy@mail.ru,24\nKarla,kitty@yahoo.com,32" > db.csv
```
Import csv to mongodb
```bash
mongoimport -d mydb -c things --type csv --file db.csv --headerline
```
## 3. Simple query
Open mongo shell
```bash
mongosh
```
mongoshell
```bash
use mydb
show dbs
use mydb;
db.things.find( { Name: "John Doe"} )
```
## 4. Call from Django

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")

mydb = myclient ["mydb"]
mycol = mydb[" things "]
myquery = { "Name": "John Doe" }
mydoc = mycol.find( myquery )
for result in mydoc:
	print(result)
```
