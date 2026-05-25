# Mysql

Developer has chosen the database MySQL. Hence, we are trying to install it up and configure it

Steps to follow to install mysql server (database)

```
dnf install mysql-server
```
To start mysql server use the cmd 

```
systemctl enable mysqld
```

```
systemctl start mysqld
```

To check the status of the service 

```
systemctl status mysqld
```

Next, we need to change defaukt root password in order to run database service. Use the password ExpenseApp@1

```
mysql_secure_installation --set-root-pass ExpenseApp@1
```

## Verification

we can check the data by using the client package called mysql

If the clinet and server both are in single server, we can use 

```
mysql
```

if the client and server are in diff servers, then we can use

```
mysql -h <datadase pvt ip add> -u root -p<passwoed>
```

```
show databases;
```

```
use transactions;
```

```
show tables;
```

if you want to see the data from starting using the cmd (* represents from starting)

```
select * from <table name>;
```

```
select * from transactions;
```

