---
sidebar_position: 1
title: Nginx
---
Although Casdoor is a front-end back-end separation architecture, in the production environment, the back-end program still provides static file services for front-end files. Therefore, you can use reverse proxy software such as [Nginx](https://www.nginx.com/) to proxy all traffic for the Casdoor domain and redirect it to the port monitored by the backend go program.

In this chapter you will learn how to use Nginx to reverse proxy your backend Go program, quickly start the Casdoor service.

## 1. Build front end static files

Now assume that you have downloaded Casdoor and completed the necessary configuration. If not, go to **Get started** section.

You only needs to build static files, like this:

```sh
cd web/
npm install && npm run build
```

## 2. Run the back end program

```sh
go run main.go
```

Or build first:

```sh
go build && ./main
```

## 3. Configure and run Nginx

```sh
vim /path/to/nginx/nginx.conf
```

Add a server:

```nginx
server {
    listen 80;
    server_name YOUR_DOMAIN_NAME;
    location / {
        proxy_set_header    Host            $http_host;
        proxy_set_header    X-Real-IP       $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_redirect      off;
        proxy_pass http://127.0.0.1:8000;
    }
}
```

Then restart your nginx process, in CentOS7, run:

```sh
systemctl restart nginx
```

## 4. Try to visit

Visit `http://YOUR_DOMAIN_NAME` in your favorite browser.