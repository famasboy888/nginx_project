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

        location /fruits {
                root /home/debian/mysite;
                try_files /vegetables/veggies.html /index.html =404     <== Try looking for veggies.html. If not, redirect to main index.html. Else throw 404 error.
        }
}

```


## Rewrites and redirects


