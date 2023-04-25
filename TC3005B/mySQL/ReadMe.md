# mySQL Tutorial

1. Download and install from 

https://dev.mysql.com/downloads/

2. Open terminal and run:

```bash
mysql -u root -p
```

3. mySQL CLI
```bash
USE mysql;
CREATE USER "tc3005b"@"localhost" IDENTIFIED BY "!Tec2023";
GRANT ALL ON *.* TO "tc3005b"@"localhost";
FLUSH PRIVILEGES;
exit
```

4. Import CSV

```csv
Alan,al@gmail.com,22,M
Melisa,mel@yandex.ru,23,F
Lisa,lis@mail.ru,21,F
Carlo,carls@yahoo.com,28,M
```
Run terminal
```bash
mysql -u tc3005b -p
```
Run mySQL CLI
```bash
SET GLOBAL local_infile=1;
```
Run terminal
```bash
mysql -u tc3005b -p --local_infile=1 newDB -e "LOAD DATA LOCAL INFILE 'newDB.csv' INTO TABLE General FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'"
```
