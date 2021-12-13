# WordPress with apache2 setup

## Code Editor

This is a very short tutorial about how to get WordPress permalinks links to work in Ubuntu 18.04/20.04 with apache2.

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

We are all done with the command line prompt.

## WordPress Dashboard

### 6. Go into your WordPress admin panel 

Go to the `Settings -> Permalinks` and select the permalink format of your choice. 

Hit the "Save Changes" button.

### 7. Done

Go to your site and check any page (other than your homepage) to ascertain that everything is working as expected.
