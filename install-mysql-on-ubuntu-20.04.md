## Install MySQL on Ubuntu 20.04 <br/><br/>

### Step 1 - Install MySQL 8 

- Start by updating the packages to the latest version available.

```bash
sudo apt update
sudo apt upgrade
```

- In Ubuntu 20.04 MySQL 8 is included by default in the Focal Fossa repositories, so you can install it easily using the apt install command.

```bash
sudo apt install mysql-server
```

Once the installation is completed, the MySQL service will start automatically. To verify that the MySQL server is running, type:

``` bash
sudo service mysql status
```

The output should show that the service is enabled and running:

```bash
 ● mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2020-05-05 07:13:18 UTC; 1min 4s ago
   Main PID: 3333 (mysqld)
     Status: "Server is operational"
      Tasks: 38 (limit: 2010)
     Memory: 322.9M
     CGroup: /system.slice/mysql.service
             └─3333 /usr/sbin/mysqld 
```

### Step 2 - Securing MySQL

- MySQL installation comes with a script named `mysql_secure_installation` that allows you to easily improve the MySQL server security.

```bash
sudo mysql_secure_installation
```

- You will be asked to configure the `VALIDATE PASSWORD PLUGIN` which is used to test the strength of the MySQL users passwords and improve the security.

```bash
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: 
```

- Press `y` if you want to set up the validate password plugin or any other key to move to the next step.

- There are three levels of password validation policy, low, medium, and strong.

```bash
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 
```

- Enter `2` for strong password validation.

- On the next prompt, you will be asked to set a password for the MySQL root user.

```bash
Please set the password for root here.
If you set up the validate password plugin, the script will show you the strength of your new password. Type y to confirm the password.

Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) :
```

- Next, you’ll be asked to remove the anonymous user, restrict root user access to the local machine, remove the test database, and reload privilege tables. You should answer `y` to all questions.


### Step 3 - Login to MySQL as root

- In MySQL 8.0, the root user is authenticated by the `auth_socket` plugin by default.

- The `auth_socket` plugin authenticates users that connect from the `localhost` through the Unix socket file. This means that you can’t authenticate as root by providing a password.

- To log in to the MySQL server as the root user, execute the following command.

```bash
sudo mysql
```

- You will be presented with the MySQL shell, as shown below:

```bash
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.20-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

- Now you can change the authentication type which helps you to login to your MySQL server as root using an external program such as phpMyAdmin.

- You can do this using two methods listed below.

### Step 4 - Create user

```sql
-- create 2 account same name and password but different host
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';   -- user for local host
CREATE USER 'admin'@'%' IDENTIFIED BY 'password';           -- user for remote

-- grant privileges
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;
```

### Step 5 - Enable remote

- When MySQL server installs, it is accessible from a local machine only. You can change this setting in the MySQL configuration file to allow remote access. Enter the following command to open MySQL configuration file in gedit or any other text editor.

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

- Change the following IP, save the file, and close it.

```
bind-address = 127.0.0.1 to 0.0.0.0
```

![desc](/img/bind-address.png "Logo Title Text 1")

- You can also change startup settings of MySQL after system boot-up through the systemctl commands

```bash
sudo systemctl enable mysql
```

- You will need to restart mysql service to take effect of all the changes to do that execute the following command in your terminal window

```bash
sudo systemctl restart mysql
```

- You should make sure that the firewall doesn’t stop incoming connections from SQL port that port 3306. For this purpose, you should give the following command in the terminal window.

```bash
sudo ufw allow from any to any port 3306 proto tcp
```

### References

- [How to Install MySQL on Ubuntu 20.04](https://www.cloudbooklet.com/how-to-install-mysql-on-ubuntu-20-04)
- [How to install and set up MySQL Database on Ubuntu 20.04](https://linuxhint.com/install_mysql_ubuntu_20-04)