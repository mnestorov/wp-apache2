# WordPress with apache2 setup

A very short tutorial about how to setup WordPress with apache2 on localhost.

## Setup a custom Localhost URL

**Hint:** *The computer file hosts is an operating system file that maps hostnames to IP addresses. It is a plain text file*

When we have a custom localhost URL, e.g `local.project-name.com`, you need to setup a custom hosts and adjust your server details.

## Update the hosts file

Every time you setup a new project, you have to update your server and hosts setup in order to use it’s domain. 
Most often a domain like that would be something like `local.sample.com`

**Hosts file location:**

- **Windows:** `c:\windows\system32\drivers\etc\hosts`
- **Mac or Linux:** `/etc/hosts`

**Open the file as an administrator/root and paste the following:**

`127.0.0.1 local.project-name.dev`

The next step is to adjust the server configuration.

## Apache Setup

For Linux and Mac, the apache config for should be found at `/etc/apache2/apache2.conf` with your standard setup. Of course, depending on the way you’ve set your stack, it could be elsewhere.

For Windows users again, it depends on your setup. If you are using Xampp, add the code in `apache/conf/extra/httpd-vhosts.conf`.

**This is working just fine for Unix like OS:**

```
<VirtualHost *:80>
    DocumentRoot /var/www/html/project-name-directory/ # update this line, based on your localhost setup/location
    ServerName local.project-name.com
    ServerAlias local.project-name.com

   <Directory /var/www/html/project-name-directory/> # update this line, based on your localhost setup/location
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
    </Directory>
</VirtualHost>
```

**This is working just fine for Windows:**

```
<VirtualHost dev.project-name.local:80>
    ServerName <project-name-here>  ## it might be something like local.project-name.com

    ServerAdmin webmaster@localhost
    DocumentRoot "C:/xampp/htdocs/<project-name>"

    <Directory "C:/xampp/htdocs/<project-name>">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```
**Important:** You will need to reset your permalinks!

## Reset permalinks in WordPress

To get WordPress permalinks links to work in Ubuntu 18.04/20.04 with apache2 we need to follow the steps bellow.

### 1. Create a .htaccess file

Manually create a `.htaccess` file and save it in your main WordPress directory.

## Terminal

### 2. Go to the terminal

**Type the following command:**

```bash
sudo chown -v :www-data "/enterYourFilePathHere/.htaccess"
```

**Hint:** You should see a line printed saying that the (group) file ownership has been changed to www-data (apache2).

### 3. Give apache2 write access to the file

**Type the following command:**

```bash
sudo chmod -v 664 "/enterYourFilePathHere/.htaccess"
```

**Hint:** You should see a line printed saying that the mode of the file has been retained.

### 4. Allow WordPress to write to the .htaccess

We have to allow WordPress to write to the `.htaccess` file by enabling `mod_rewrite` in the apache2 server. 

**Type the following command:**

```bash
sudo a2enmod rewrite
```
You should see a line printed saying that it is enabling `mod_rewrite` and reminding you to restart the web server.

### 5. Restart the web server

Restart the web apache2 for the changes to take effect.

**Type the following command:**

```bash
sudo /etc/init.d/apache2 restart
```

OR

```bash
sudo service apache2 restart
```

We are all done with the command line prompt.

## WordPress Dashboard

### 6. Go into your WordPress admin panel 

Go to the `Settings -> Permalinks` and select the permalink format of your choice. 

Hit the "Save Changes" button.

### 7. Done

Go to your site and check any page (other than your homepage) to ascertain that everything is working as expected.
