# How to replicate ThingWiki

Documentation on how to replicate the ThingWiki prototype. This document is derived from the documentation of the fonte.wiki project crafted by [Tiago Bugarin](https://github.com/tiagobugarin).

1. Set up a Virtual Private Server using Ubuntu or Debian as OS on your preferred hosting provider.
2. Access your VPS:
   - ssh -i path/to/your/ssh/key.pub root@ip-address-of-your-VPS
3. Make sure the system is up to date
   - apt update && apt upgrade -y
3. Enable the server to listen on ports 80 and 443
   - sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
   - sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
4. Install netfilter-persistent to make the port changes persistent
   - sudo apt install netfilter-persistent -y
   - sudo netfilter-persistent save
5. (Uninstall and) install docker. Make sure to edit the code below to match the distro you are using (debian or ubuntu)

```
sudo apt remove docker docker-engine docker-compose docker.io containerd runc

sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee \
  /etc/apt/sources.list.d/docker.list > /dev/null

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o \
  /usr/share/keyrings/docker-archive-keyring.gpg

sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io docker-compose -y

```

6. Add a new group called docker to the system:


```
sudo usermod -aG docker $USER

newgrp docker
```

7. Create a working folder and change into it

```
mkdir thingwiki
cd thingwiki
```

8. Create a random password for the database:

```
sudo apt install pwgen -y

echo $(pwgen -cnys 64 1) > postgres_pwd.pw
```

9. NginX main server configuration

nano nginx-main.conf

Paste the following code:

events { worker_connections 1024; }
http {
  server {
    listen 80;
    listen [::]:80;
    location / {
      proxy_pass http://wikijs-main:3000;
      proxy_http_version 1.1;
    }
  }
}

10. Edit the file docker-compose.yml. Make sure to edit the code below to include your email and to match the domain name to generate the proper encryption keys and allow the site to use HTTPS.

```
version: '3.6'

services:
  # Start access server configuration
  nginx-proxy:
    image: nginxproxy/nginx-proxy:0.9-alpine
    container_name: nginx-proxy
    restart: unless-stopped
    #logging:
      #driver: "none"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - certs:/etc/nginx/certs
      - vhost:/etc/nginx/vhost.d
      - html:/usr/share/nginx/html
      - dhparam:/etc/nginx/dhparam
      - /var/run/docker.sock:/tmp/docker.sock:ro

  nginx-proxy-acme:
    image: nginxproxy/acme-companion:2.1
    container_name: nginx-proxy-acme
    restart: unless-stopped
    #logging:
      #driver: "none"
    environment:
      - DEFAULT_EMAIL=your@email.address
      - NGINX_PROXY_CONTAINER=nginx-proxy
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - acme:/etc/acme.sh
      - certs:/etc/nginx/certs
      - vhost:/etc/nginx/vhost.d
      - html:/usr/share/nginx/html
  # End access server configuration

  # Start appl configuration
  nginx-main:
    image: nginx:mainline-alpine
    container_name: nginx-main
    restart: unless-stopped
    #logging:
      #driver: "none"
    depends_on:
      - wikijs-main
    environment:
      - VIRTUAL_HOST=your.domain.name
      - LETSENCRYPT_HOST=your.domain.name
    volumes:
      - ./nginx-main.conf:/etc/nginx/nginx.conf:ro

  wikijs-main:
    image: requarks/wiki:2
    container_name: wikijs-main
    restart: unless-stopped
    #logging:
      #driver: "none"
    depends_on:
      - postgres-main
    ports:
      - "3000:3000"
    environment:
      DB_TYPE: postgres
      DB_HOST: postgres-main
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS_FILE: /run/secrets/postgres-user-pwd
      DB_NAME: wikijs
    volumes:
      - conteudo-wikijs-main:/wiki/data/content
    secrets:
      - postgres-user-pwd

  postgres-main:
    image: postgres:13-alpine
    container_name: postgres-main
    restart: unless-stopped
    #logging:
      #driver: "none"
    environment:
      POSTGRES_DB: wikijs
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres-user-pwd
      POSTGRES_USER: wikijs
    volumes:
      - postgres-data-main:/var/lib/postgresql/data
    secrets:
      - postgres-user-pwd
  # End app configuration

volumes:
  postgres-data-main:
  conteudo-wikijs-main:
  # don't edit the volumes below - they are needed for nginx-proxy and nginx-proxy-acme
  certs:
  vhost:
  html:
  dhparam:
  acme:

secrets:
  postgres-user-pwd:
    file: ./postgres_pwd.pw

```

11. docker-compose up -d

12. Fork the Thingwiki repository on GitHub

https://github.com/reuse-city/thingwiki

13. Follow the instructions on wiki.js documentation to use git storage and synchronize it with your working copy of the Thingwiki repository

https://docs.requarks.io/storage/git
