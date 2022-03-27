# Opactyl-0.1
We cannot force you to keep the "Powered by Opactyl" in the footer, but please consider keeping it. It helps getting more visibility to the project and so getting better. We won't do technical support for installations without the notice in the footer.

# Installation Guide
# Install Guide (pt. 1)

Head over to the Wiki page to see how to install Opactyl.
Or join our discord if help is needed (:
Warning: You need Pterodactyl already set up on a domain for Opactyl to work
Main Commands:
1.Run :`sudo apt update && sudo apt upgrade`on the vps

2.Run: `sudo apt install git`on the vps

3.Run: `curl -fsSL https://deb.nodesource.com/setup_12.x | sudo bash -`on the vps

4.Run: `apt install nodejs`on the vps

5. Run: `npm -v` on the vps

6.Run: `mkdir -p /var/www/`on the vps

7.Run: `cd /var/www/`on the vps

8.Run `git clone https://github.com/VedangOp/Opactyl-0.1.git`on the vps

9. Run `cd Opactyl-0.1`on the vps
 
10. Run `nano settings.json` on the vps and config it!

 TIPS:
1. Upload the file above onto a Pterodactyl NodeJS server [Download the egg from Parkervcp's GitHub Repository](https://github.com/parkervcp/eggs/tree/master/bots/discord/discord.js)
2. Unarchive the file and set the server to use NodeJS 12
3. Configure settings.json (specifically panel domain/apikey and discord auth settings for it to work)
4. Start the server (Ignore the 2 strange errors that might come up)

# Install Guide (pt. 2)


1. Login to your DNS manager, point the domain you want your dashboard to be hosted on to your VPS IP address. (Example: dashboard.domain.com 192.168.0.1)
2. Run `apt install nginx && apt install certbot` on the vps
3. Run `ufw allow 80` and `ufw allow 443` on the vps
4. Run `certbot certonly -d <Your Opactyl Domain>` then do 1 and put your email
5. Run `nano /etc/nginx/sites-enabled/opactyl.conf`
6. Paste the configuration at the bottom of this and replace with the IP of the pterodactyl server including the port and with the domain you want your dashboard to be hosted on.
7. Run `systemctl restart nginx` and try open your domain.
# Nginx Proxy Config
```Nginx
server {
    listen 80;
    server_name <domain>;
    return 301 https://$server_name$request_uri;
}
server {
    listen 443 ssl http2;
location /afkwspath {
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
  proxy_pass "http://localhost:<port>/afkwspath";
}
    
    server_name <domain>;
ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
location / {
      proxy_pass http://localhost:<port>/;
      proxy_buffering off;
      proxy_set_header X-Real-IP $remote_addr;
  }
}
```
