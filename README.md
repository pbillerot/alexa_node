# alexa_node
Serveur de Son de batteries et Skill Alexa

> Version non fonctionnelle

## NGINX

    sudo apt install nginx

### nginx.conf
```
upstream mondomaine_fr {
    server localhost:4000;
}

server {

  listen 80;
  listen [::]:80; 
  listen 443 ssl http2;
  listen [::]:443 ssl http2;

  server_name mondomaine.fr;

  ssl_certificate /etc/letsencrypt/live/domain.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/domain.com/privkey.pem;

  location / {
    proxy_pass http://mondomaine_fr;
  }

  location /websocket/ {
    proxy_pass http://mondomaine_fr;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
  }

}
```

## PM2
https://www.yubigeek.com/pm2-gestionnaire-processus-nodejs/

```bash
sudo npm install -g pm2
sudo pm2 startup
sudo pm2 start index.js
sudo pm2 save
```

## CERTBOT
```
sudo apt install certbot
sudo certbot certonly --standalone -d domain.com --rsa-key-size 4096
```
