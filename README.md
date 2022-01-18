# Script-who-to-deploy-laravel-app-in-NEW-server-with-mongo-db

Step 1 — Installing Package Dependencies

To run Laravel applications, you’ll need some PHP extensions and a PHP dependency manager called Composer in addition to the basic LEMP stack.
Start by updating the package manager cache.
```
sudo apt-get update
```
The PHP extensions you’ll need are for multi-byte string support and XML support. You can install these extensions, Composer, and unzip (which allows Composer to handle zip files) at the same time.
```
sudo apt-get install php7.4-mbstring php7.4-xml composer unzip
```
Step 3 — Setting Up the Demo Application

The demo quickstart application, distributed by Laravel on GitHub.
Move to the new directory and clone the demo application using Git.
```
cd /public_html
git clone https://github.com/laravel/xxxxxxxxxx .
```

Step 4 — Configuring the Application Environment

In this step, we’ll modify some security-related application settings, allow the application to connect to the database, and prepare the database for usage. These are necessary steps for all LEMP-backed Laravel applications, not just the demo application we’re using here.

Open the Laravel environment configuration file with nano or your favorite text editor.
```
sudo nano /var/www/html/quickstart/.env
```
Step 5 - 

Next, we need to install the project dependencies. Laravel utilizes Composer to handle dependency management, which makes it easy to install the necessary packages in one go.
```
composer install
```

>in case of any error install these dependies (*)recomended commands
```
sudo apt install php7.4-fpm
sudo add-apt-repository ppa:ondrej/php
sudo apt-get install php7.4-mongodb
sudo apt-get install php7.4-dev
sudo apt install php-xml
sudo apt install php7.4-gd
sudo apt install php7.4-mbstring
sudo apt install php7.4-zip
sudo pecl install mongodb
sudo apt install mongodb
```
```
sudo apt-get install php7.4-curl
```
```
*composer update
```

Visit= https://www.digitalocean.com/community/tutorials/how-to-deploy-a-laravel-application-with-nginx-on-ubuntu-16-04


-------------------------------------------------------------------------------------------------------



> Error = 1
```
80 packages you are using are looking for funding.
Use the command to find out more!
```
>more details
```
root@eod:/home/eodmt/public_html/eod-mt# composer install
Do not run Composer as root/super user! See https://getcomposer.org/root for details
Loading composer repositories with package information
Installing dependencies (including require-dev) from lock file
Nothing to install or update
Package fzaninotto/faker is abandoned, you should avoid using it. No replacement was suggested.
Package swiftmailer/swiftmailer is abandoned, you should avoid using it. Use symfony/mailer instead.
Generating optimized autoload files
composer/package-versions-deprecated: Generating version class...
composer/package-versions-deprecated: ...done generating version class
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi
Discovered Package: facade/ignition
Discovered Package: fideloper/proxy
Discovered Package: fruitcake/laravel-cors
Discovered Package: jenssegers/mongodb
Discovered Package: laravel/tinker
Discovered Package: laravel/ui
Discovered Package: nesbot/carbon
Discovered Package: nunomaduro/collision
Discovered Package: realrashid/sweet-alert
Package manifest generated successfully.
80 packages you are using are looking for funding.
Use the `composer fund` command to find out more!
```
```
composer fund
```

>Error = 2 (php7.4-curl)
```
Problem 1
    - Installation request for multicaret/laravel-unifonic ^2.0 -> satisfiable by multicaret/laravel-unifonic[v2.0.0].
    - multicaret/laravel-unifonic v2.0.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
  
  
  Problem 2
    - pusher/pusher-php-server v5.0.1 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - pusher/pusher-php-server 5.0.x-dev requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - pusher/pusher-php-server 5.0.3 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - pusher/pusher-php-server 5.0.2 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - Installation request for pusher/pusher-php-server ^5.0.1 -> satisfiable by pusher/pusher-php-server[5.0.2, 5.0.3, 5.0.x-dev, v5.0.1].
```


visit: https://stackoverflow.com/questions/63731920/is-there-a-way-to-hide-funding-messages-when-running-composer-commands


