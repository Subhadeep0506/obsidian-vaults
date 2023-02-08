# Install
```bash 
sudo nala install mysql-server
```
# Configure
- Run Mysql as root-
`sudo mysql`
- Then run the command-
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
and exit with `exit` command
-  Then run `sudo mysql_secure_installation` to setup mysql
# Creating a Dedicated MySQL User and Granting Privileges
- Login to mysql - `mysql -u root -p`
- Create users and add privileges
``` sql
CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password'; 
CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';
````
- Grant privilages to database 
```sql
GRANT PRIVILEGE ON database.table TO 'username'@'host';
```
```sql
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
```
# MySQL in RapberryPi Manjaro
1. Installation:
`sudo pacman -S mysql`
2. Start the services:
```bash
sudo systemctl start mysqld
sudo systemctl status mysqld
```
If errors occurs:
```bash
sudo rm -rf /var/lib/mysql
sudo mysql_install_db --user=mysql --basedir=/usr - datadir=/var/lib/mysql
```
...and then again start services.
3. `sudo mysql_secure_installation`  to setup
4. Now create user:
`sudo mysqld`
````sql
CREATE USER 'subhadeep'@'localhost' IDENTIFIED BY 'pillsgap';
GRANT ALL PRIVILEGES ON *.* TO 'subhadeep'@'localhost' WITH GRANT OPTION;
````
5. To allow access to databases from all devices:
````sql
CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost' WITH GRANT OPTION;
CREATE USER 'monty'@'%' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'monty'@'%' WITH GRANT OPTION;
````