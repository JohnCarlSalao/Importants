


# Deploy a Git Repository to `/var/www/html` and Serve with Nginx

  

## 🛠 Step 1: SSH into the Server

If you’re working on a remote server, connect via SSH:

```sh

ssh user@your-server-ip
```

📦 Step 2: Install Required Packages

Ensure you have Git and Nginx installed. If not, install them:

  

```sh
sudo apt update && sudo apt install -y git nginx
```
📂 Step 3: Clone the Repository to /var/www/html

Clone your repository:

```sh
sudo git clone <your-repo-url> /var/www/html/your-project
```
If the directory already exists, update it:

  
```sh
cd /var/www/html/your-project
sudo git pull origin main
```

🔑 Step 4: Set Permissions

Set the correct ownership and permissions for Nginx:

  
```sh

sudo chown -R www-data:www-data /var/www/html/your-project

sudo chmod -R 755 /var/www/html/your-project
```

⚙️ Step 5: Configure Nginx

Create a new Nginx configuration file:

```sh

sudo nano /etc/nginx/sites-available/your-project
```


Add the following content:

  

nginx

```sh

server {

    listen 80;

    server_name angeles.comclark.com;

  

    root /var/www/angeles;

    index index.html;

  

    return 301 https://$host$request_uri;

  

    location / {

        try_files $uri /index.html;

    }

  

}

  

server {

    listen 443 ssl;

    server_name angeles.comclark.com;

  

    root /var/www/angeles;

    index index.html;

  

    ssl_protocols TLSv1.2 TLSv1.3;

    ssl_prefer_server_ciphers on;

    ssl_ciphers "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH";

  

    ssl_certificate /etc/nginx/ssl/fullchain.crt;

    ssl_certificate_key /etc/nginx/ssl/comclark.key;

    ##Mod Security

    modsecurity on;

    modsecurity_rules_file /etc/nginx/modsec/main.conf;

  

    location / {

        try_files $uri /index.html;

    }

  

}

```

Save and exit (CTRL+X, then Y, then ENTER).

  

🔗 Step 6: Enable the Site and Restart Nginx

```sh

sudo ln -s /etc/nginx/sites-available/your-project /etc/nginx/sites-enabled/

sudo nginx -t # Test the configuration

sudo systemctl restart nginx

🔥 Step 7: Open the Firewall

If using UFW, allow HTTP and HTTPS traffic:
```

  

```sh
sudo ufw allow 'Nginx Full'
```


🌐 Step 8: Test in the Browser

Open your browser and visit:

  
  
  

http://your-server-ip

or

  
  

http://your-domain.com