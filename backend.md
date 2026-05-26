# Backend

Backend is responsible for adding values to datbase. Backend service is writen in nodejs.

**Backend progamming language and version will be decided by the developer, In this developer has set a context that it can work with nodejs ver20**

By default nodejs 16 is avaliable, wee need to install nodejs version 20 and install it.

**Steps to follow to install nodejs**

**First disable the default ver., then enable required vers. and install it**

```
dnf module disable nodejs -y
```

```
dnf module enable nodejs:20 -y
```

```
dnf install nodejs -y
```

Configure the application

Add a user to the application 

```
useradd expense
```

create a directory with /app name 

```
mkdir /app
```

**Download the application code to created app directory**

First we need to download the code to the tmp directory and will unzip the code to the respective created app directory

```
curl -o /tmp/backend.zip https://expense-joindevops.s3.us-east-1.amazonaws.com/expense-backend-v2.zip
```
go to app directory

```
cd /app
```
unzip the code 

```
unzip /tmp/backend.zip/
```
Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.

Lets download the dependencies.

```
cd /app
```
```
npm install
```

we need to setup a new service in systemd so systemctl can manage this service

Setup SystemD Expense Backend Service

```
vim /etc/systemd/system/backend.service
```

```
[Unit]
Description = Backend Service

[Service]
User=expense
Environment=DB_HOST="<MYSQL-SERVER-IPADDRESS>"
ExecStart=/bin/node /app/index.js
SyslogIdentifier=backend

[Install]
WantedBy=multi-user.target
```

**NOTE: Ensure you replace <MYSQL-SERVER-IPADDRESS> with IP address (pvt ip add.)**

Load the service.

```
systemctl daemon-reload
```

start the service

```
systemctl enable backend
```

```
systemctl start backend
```

For this application to work fully functional we need to load schema to the Database.

We need to load the schema. To load schema we need to install mysql client.

To have it installed we can use

```
dnf install mysql -y
```

load schema

```
mysql -h <mysql-server-ipaddress> -uroot -pExpenseApp@1 < /app/schema/backend.sql
```

Restart the service

```
systemctl restart backend
```

To check the status of the service
```
systemctl status backend
```

to check process

```
ps -ef | grep backend
```

to check the ports

```
netstat -lntp
```

to check whether backend service is conneced to database or not 

telnet database pvt.ipadd. <portno>

```
telnet dbip portno
```


