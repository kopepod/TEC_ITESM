# Server-side installations

1. Apache

```bash
sudo apt update && sudo apt upgrade
sudo apt install apache2 libapache2-mod-php mysql-server mysql-client php-mysql
sudo ufw app list
sudo ufw allow 'Apache'
sudo ufw status
sudo systemctl restart apache2
firefox http://localhost
```

2. MySQL

```bash
sudo apt-get install mysql-server
sudo ufw allow mysql
systemctl start mysql
sudo systemctl enable mysql
sudo mysql_secure_installation
mysql -u root -p
```

3. NodeJS support for mySQL

```bash
sudo apt install nodejs
sudo apt install npm
npm install express mysql
wget https://atom.io/download/deb
sudo dpkg -i atom-amd64.deb
npm install html-template-generator
```

4. Github

```bash
sudo apt install git
git init Mytest
cd Mytest
gedit README
gedit code.c
git add README
git add code.c
git commit -m "some_message"
git remote add origin https://github.com/user_name/Mytest.git
git push origin master
```

5. Django + mongoDB

```bash
sudo apt install python3-django
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
sudo apt-get install gnupg
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
sudo systemctl status mongod
```
