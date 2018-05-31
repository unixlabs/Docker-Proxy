# Docker-Proxy
Docker Proxy: Cache your images on your local data center save your Bandwidth.   In Simple its docker registry that Cache images on self hosted network.

# How its Works
Docker Proxy works as caching server during your pull reqest to an image, its save the image in the cache, in case you can run again pull request then you can you find these iamges in your local registry. its work as mirror and save all iamges that you pull through the proxy.  
# Prerequisite 
> Running Docker with Docker Compose
```sh
curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` > ./docker-compose
mv ./docker-compose /usr/bin/docker-compose
chmod +x /usr/bin/docker-compose

```
# Installation 
```sh
git clone https://github.com/unixlabs/Docker-Proxy.git
cd Docker-Proxy && docker-compose up -d
```
#  Verify the container is up 

Test Docker Proxy Cache Verify that the container is up and listening on port 5000.

```sh
# curl -i http://localhost:5000/
HTTP/1.1 200 OK
Cache-Control: no-cache
Date: Thu, 31 May 2018 10:38:54 GMT
Content-Length: 0
Content-Type: text/plain; charset=utf-8
```
# Usage 
change your default mirror in your docker daemon setting like.

```sh
# nano /etc/docker/daemon.json
{
  "registry-mirrors": ["http://localhost:5000"]
}
```
# Testing 
```sh
# time docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
a48c500ed24e: Pull complete
1e1de00ff7e1: Pull complete
0330ca45a200: Pull complete
471db38bcfbf: Pull complete
0b4aba487617: Pull complete
Digest: sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
Status: Downloaded newer image for ubuntu:latest

real    0m20.766s
user    0m0.198s
sys     0m0.030s


# docker rmi ubuntu
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
Deleted: sha256:452a96d81c30a1e426bc250428263ac9ca3f47c9bf086f876d11cb39cf57aeec
Deleted: sha256:96fccbf869d3c0ee0fb2e976fdf356dc5872f6410030fd094bbc5b34a7559cdb
Deleted: sha256:38ffa1479cb9fd81d0d4d057c282a155a4a83bff5d2b507ee9563f996d74272d
Deleted: sha256:cc6967c5525a55626688a773e4fe578321a2e126a3b1df1bc0763cfd1583c50c
Deleted: sha256:2a2d486f02032f5a6cc56290a244512daa07a8efe0124bccc5701f0a778aa947
Deleted: sha256:65bdd50ee76a485049a2d3c2e92438ac379348e7b576783669dac6f604f6241b

# time docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
a48c500ed24e: Pull complete
1e1de00ff7e1: Pull complete
0330ca45a200: Pull complete
471db38bcfbf: Pull complete
0b4aba487617: Pull complete
Digest: sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
Status: Downloaded newer image for ubuntu:latest

real    0m5.058s
user    0m0.060s
sys     0m0.005s

# Images will be cached in Docker-Proxy/.data/ directory

```
