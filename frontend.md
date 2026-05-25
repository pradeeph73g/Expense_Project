# Frontend 

The frontend is the service in Expense to serve the web content over Nginx. This will have the web frame for the web application.

Developer has chosen Nginx as a web server and thus we will install Nginx Web Server.

Install Nginx
```
dnf install nginx -y
```
enable niginx
```
systemctl enable nginx
```
start nginx
```
systemctl start nginx
```

**Try to access the service over the browser and ensure you get some default content**

Remove the default conent 

```
rm -rf /usr/share/nginx/html/*
```

Download the frontend content

```
curl -o /tmp/frontend.zip https://expense-joindevops.s3.us-east-1.amazonaws.com/expense-frontend-v2.zip
```

Unzip the frontend content

```
cd /usr/share/nginx/html
```

```
unzip /tmp/frontend.zip
```

**Try to access the nginx service once more over the browser and ensure you get the expense content**

create nginx reverse proxy configuration

```
vim /etc/nginx/default.d/expense.conf
```

add the following content and replace with backend pvt ipadd in the place of localhost 

```
proxy_http_version 1.1;

location /api/ { proxy_pass http://localhost:8080/; }

location /health {
  stub_status on;
  access_log off;
}
```

**Ensure you replace the localhost with the actual ip address of backend component server. Word localhost is just used to avoid the failures on the Nginx Server.**

```
systemctl restart nginx
```

status check
```
systemctl status nginx
```

ensure to check whether the frontend is connected to backend

```
telnet backend ipadd <port no.>
```

