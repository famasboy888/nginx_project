# Nginx


Inside /etc/nginx/`nginx.conf`:

This key value pair is called **Directives**

`worker_connections 768;`

This block of code is called **Context**

```bash
events {
        worker_connections 768;
}
```

## Commands

`sudo nginx -s reload`

<hr>

## Create a basic server context:

This allows to specify a custom path of HTML files

```bash
http {
        server {
                listen 8080;
                root /home/debian/mysite;
        }
}
```

## Allow CSS types and other MIME.TYPES

```bash
http {
        include mime.types;                  <== Include this

        server {
                listen 8080;
                root /home/debian/mysite;
        }
}
```

## Adding Location

```bash
server {
        listen 8080;
        root /home/debian/mysite;

        location /fruits {
                root /home/debian/mysite;            <== this translates to /home/debian/mysite/fruits/index.html
        }

        location /vegetables {
                root /home/debian/mysite;
                try_files /vegetables/veggies.html /index.html =404     <== Try looking for veggies.html. If not, redirect to main index.html. Else throw 404 error.
        }
}

```


## Rewrites and redirects

`Code 307` specifies that we want to redirect it to another route.

```bash
server {
        listen 8080;
        root /home/debian/mysite;

        location /fruits {
                root /home/debian/mysite; 
        }

        location /crops {
                return 307 /fruits        <== redirect codde 307
        }
}

```
<hr>

# NGINX as LoadBalancer

This will create a round robin load balancer

```bash
http {
        include mime.types;

        upstream backendserver {                                        <== You can use any name but remember it. Name should be used in "proxy_pass" directive
                server 192.168.2.77:1111;                                <== Specify all ports here
                server 192.168.2.77:2222;
                server 192.168.2.77:3333;
                server 192.168.2.77:4444;
        }

        server {
                listen 8080;

                location / {
                        proxy_pass http://backendserver/;                <== Declare "proxy_pass" here and follow the syntax.
                }
        }
}

events {

}
```


