---
layout: post
title: Localhost with Https
subtitle: How to set up https://localhost
bigimg: ../img/analog.jpg
---

### There are some apps which require you to use https, but what if you aren't ready to deply and are still working using localhost?

There are two packages to the rescue 

[mkcert](https://github.com/FiloSottile/mkcert)
[http-server](https://www.npmjs.com/package/http-server)

The first one is used to generate the certificate and key, the second one will serve our static files using the generated files.

Let's do it.

First install [mkcert](https://github.com/FiloSottile/mkcert#installation) by following instruction from github page.

Then run in your working directory following commands:

```
mkcert -install
mkcert localhost
```

The above will create `localhost.pem` and `localhost-key.pem` files in your directory.

Now it is time to use http-server.

To install globally run:
`npm install http-server -g`

And in your directory with files you want to serve:
`http-server .\index.html -p 9025 --ssl -K .\localhost-key.pem -C .\localhost.pem`

The above will serve your index.html file on port 9025 with ssl on using key localhost-key.pem and certificate localhost.pem.

Now you can go to https://localhost:9025
