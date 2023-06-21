

# Step 1 
##—------ UPDATE THE UBUNTU PACKEGES AND REPOSITORY---------------------------------#
```
sudo apt-get update
```
# Step 2 
##—------ GIT CLONE THE REPO--------------------------------------------------------#

The demo quickstart application, distributed by Laravel on GitHub.
Move to the new directory and clone the demo application using Git.
```
cd /public_html
git clone https://github.com/laravel/xxxxxxxxxx .
```
**OR**
you can create the new laravel project my the boiler-plate command:
```
composer create-project --prefer-dist laravel/laravel <project-name>
```

# Step 3 
##—------ CONFIGURE THE SECURIT/.ENV FILE FOR PROJECT-------------------------------#
In this step, we’ll modify some security-related application settings, allow the application to connect to the database, and prepare the database for usage. These are necessary steps for all LEMP-backed Laravel applications, not just the demo application we’re using here.

Open the Laravel environment configuration file with nano or your favorite text editor.
```
sudo nano /var/www/html/quickstart/.env
```
# Step 4 
##—------ INSTALL PHP/LARAVEL AND SOME PACKEGES-------------------------------------#

we need to install the project dependencies. Laravel utilizes Composer to handle dependency management, which makes it easy to install the necessary packages in one go.

**vist to install latest composer version** : https://github.com/SyedAsadRazaDevops/How-to-install-latest-version-compoer-for-Laravel-on-ubuntu

in case of any error install these dependies (*)recomended commands
>FOR PHP-7.4 INSTALLATION PROCESS
```
sudo apt-get install software-properties-common
sudo add-apt-repository --yes ppa:ondrej/php
sudo apt-get install php7.4-curl -y
sudo apt install php7.4-fpm -y
sudo add-apt-repository --yes ppa:ondrej/php
sudo apt-get install php7.4-mongodb -y
sudo apt-get install php7.4-dev -y
sudo apt install php7.4-xml -y
sudo apt install php7.4-gd -y
sudo apt install php7.4-mbstring -y
sudo apt install php7.4-zip -y
```
>FOR PHP-8.1 INSTALLATION PROCESS
```
sudo apt-get install software-properties-common
sudo add-apt-repository --yes ppa:ondrej/php
sudo apt install php8.1-fpm -y
sudo apt-get install php8.1-mongodb -y
sudo apt-get install php8.1-dev -y
sudo apt install php8.1-xml -y
sudo apt install php8.1-gd -y
sudo apt install php8.1-mbstring -y
sudo apt install php8.1-zip -y
sudo apt-get install php8.1-curl -y
```
>FOR PHP-8.2 INSTALLATION PROCESS
```
sudo apt-get install software-properties-common
sudo apt install php8.2-fpm -y
sudo apt-get install php8.2-mongodb -y
sudo apt-get install php8.2-dev -y
sudo apt install php8.2-xml -y
sudo apt install php8.2-gd -y
sudo apt install php8.2-mbstring -y
sudo apt install php8.2-zip -y
sudo apt-get install php8.2-curl -y
```
**you can switch the alternative PHP vertion in ubuntu, if you already had installed:** `sudo update-alternatives --config php`
<img width="929" alt="Screenshot 2022-12-27 at 2 52 56 PM" src="https://user-images.githubusercontent.com/71556060/209648487-4d7c36aa-3fcc-46ac-a020-334b79b36a93.png">

# Step 4.5
##—------ INSTALL LATEST COMPOSER IN UBUNTU --------------#

[How-to-downgrade-or-install-a-specific-version-of-Composer](https://github.com/SyedAsadRazaDevops/How-to-install-latest-version-compoer-for-Laravel-on-ubuntu)

# Step 5 
##—------ INSTALL MONGODB DATABASE YOU CAN USE MYSQL DEPEND ON PROJECT--------------#
### Install MongoDB 5 on Ubuntu 20.04|

**To install the latest version of mongodb, use this link: ** https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/

Import the public key used by the package management system.
```
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```
```
sudo apt-get install gnupg
```
Create a list file for MongoDB
```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```
Reload local package database.
```
sudo apt-get update
```
Install the MongoDB packages.
```
sudo apt-get install -y mongodb-org
```
Start MongoDB.
```
sudo systemctl start mongod
```
If you receive an error
```
sudo systemctl daemon-reload
or
sudo systemctl start mongod
```
Verify that MongoDB has started successfully.
```
sudo systemctl status mongod
sudo systemctl enable mongod
```

### Uninstall mongodb
**OR IN-CASE TO REINSTALL AND UPGRAGE THE DATABASE**
First list all packages that contain mongo in their names or their descriptions):
```
dpkg -l | grep mongo
```
Go to /tmp and find mongodb sock
```
cd /tmp; ls -l *.sock
```
In summary, I would do (to purge all packages that start with mongo):
```
sudo apt purge mongo*
```
and then (to make sure that no mongo packages are left):
```
dpkg -l | grep mongo
```
```
sudo apt-get install mongodb-org --fix-missing --fix-broken
sudo apt-get autoremove mongodb-org --fix-missing --fix-broken
```

# Step 6 
##—------ RUN THESE COMMAND TO CLEAR CACHE AND ETC--------------------------------#
```
sudo php artisan config:clear
sudo php artisan config:cache
sudo php artisan optimize:clear
sudo php artisan cache:clear
sudo composer dump-autoload
sudo php artisan view:clear
sudo php artisan route:clear
```
OPPTINAL(some data-seeder/migration command depend on developers)
```
php artisan make:admin
php artisan add:data
```
```
mkdir -p storage/framework/sessions
mkdir -p storage/framework/views
mkdir -p storage/framework/cache
```
# Step 7
##—------ CONFIGRATION BLOCK FOR SERVER NGINX-------------------------------------#

**To install the latest version of nginx, use this link: ** https://github.com/SyedAsadRazaDevops/who-to-install-and-upgrade-nginx-1.20-on-Ubuntu-20.04

Once on the server, look for your web server configuration in /etc/nginx/sites-enabled. There is also a directory called sites-allowed; this directory includes configurations that are not necessarily activated. Once you find the configuration file, display the output in your terminal with the following command:
```
cat /etc/nginx/sites-enabled/your_domain
```
If your site has no HTTPS certificate, you will receive a result similar to this:

Output
```
server {
    listen 80;
    listen [::]:80;
    server_name <my-domain> www.<my-domain>;
    root <my-project-path>/public;
    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }

}

```
Next, you need to create a symbolic link within the sites-enabled directory that points out to this configuration file:
```
sudo ln -s /etc/nginx/sites-available/<my-nginx-file-name> /etc/nginx/sites-enabled
```
>Make sure to check that there are no syntax errors in the configuration.
```
sudo nginx -t
```
If all changes were successful, you will get a result that looks like this:
>Output
```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
If that is the case, you can safely restart Nginx to put the changes in effect.
```
sudo systemctl restart nginx
```
# Check what user PHP-FPM is running as (it's www-data)
```
ps aux | grep php
```

# Assing permisstion to these files:
```
sudo chmod -R 775 ./storage
sudo chmod -R 775 ./bootstrap/
```
# Step 7
##—------ INSTALL CERTBOT FOR SSL NGINX-------------------------------------#
```
sudo apt install snapd
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
GENRATE SSL FOR DOMAINS
```
sudo certbot --nginx
```

##—------ DONE------------------------------------------------------------------#

### IF YOU WANT TO INCRESS THE LIMIT OF PHP:
PATH > /etc/php/7.4/fpm/php.ini
```
;;;;;;;;;;;;;;;;;;;
; Resource Limits ;
;;;;;;;;;;;;;;;;;;;

max_execution_time = 12000
max_input_time = 12000
memory_limit = 8192M
```

### IF YOU WANT TO INCRESS THE LIMIT OF NGINX:
PATH >  /etc/nginx/site-avalible/mydomail.com
under location block:
        
```
 location / {
            proxy_read_timeout 1800;
            proxy_connect_timeout 1800;
            proxy_send_timeout 1800;
            send_timeout 1800;
            client_max_body_size 8048M;
 ```
So i have to adjust the **fastcgi_read_timeout** in my server configuration: 
```
location ~ \.php$ {
     fastcgi_read_timeout 240;
     ...
 }
``` 


visit: https://stackoverflow.com/questions/63731920/is-there-a-way-to-hide-funding-messages-when-running-composer-commands


