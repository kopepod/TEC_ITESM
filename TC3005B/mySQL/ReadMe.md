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
