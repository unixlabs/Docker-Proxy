# Docker-Proxy
Docker Proxy: Cache your images on your local data center save your Bandwidth.   In Simple its docker registry that Cache images on self hosted network.
# Prerequisite 
> Running Docker with Docker Compose
# Installation 
```sh
git clone https://github.com/unixlabs/Docker-Proxy.git
cd Docker-Proxy && docker-compose up -d
```
# Testing 
Test Docker Proxy Cache, its shows running on the port 5000  
```sh
# curl -i http://localhost:5000/
HTTP/1.1 200 OK
Cache-Control: no-cache
Date: Thu, 31 May 2018 10:38:54 GMT
Content-Length: 0
Content-Type: text/plain; charset=utf-8
```
