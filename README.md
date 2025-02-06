# Setting Up PHP 8.0 with Apache on Ubuntu  

## Prerequisites  
Make sure you have a fresh Ubuntu installation with sudo access.  

---

## Step 1: Update System Packages  
Before installing new software, update your system:  
```bash
sudo apt update && sudo apt upgrade -y
```  

---

## Step 2: Install Essential Utilities  
Install required utilities such as unzip and p7zip:  
```bash
sudo apt-get install unzip -y  
sudo apt-get install p7zip -y  
```  

---

## Step 3: Install Apache Web Server  
Install Apache with the following command:  
```bash
sudo apt install apache2 -y  
```  

Check if Apache is running:  
```bash
sudo systemctl status apache2  
```  

If Apache is not active, start it using:  
```bash
sudo systemctl start apache2  
```  

---

## Step 4: Install PHP 8.0  
Add the repository that provides multiple PHP versions:  
```bash
sudo add-apt-repository -y ppa:ondrej/php  
sudo apt update  
```  

Now, install PHP 8.0:  
```bash
sudo apt install php8.0 -y  
```  

Verify the installation:  
```bash
php -v  
```  

---

## Step 5: Install Required PHP Extensions  
Install necessary PHP extensions:  
```bash
sudo apt install php8.0-dom php8.0-gd php8.0-intl php8.0-mbstring php8.0-xml php8.0-xsl php8.0-zip -y  
sudo apt-get install php8.0-curl php8.0-pdo-mysql php8.0-bcmath -y  
```  

---

## Step 6: Set Up an API Directory  
Navigate to the web root directory and create an `/api` folder:  
```bash
cd /var/www/html/  
sudo mkdir api  
cd api  
```  

Create the `number_classify.php` file:  
```bash
sudo nano number_classify.php 
```  

Paste your `number_classify.php` script inside, then save the file (CTRL + X, then Y, then ENTER).  

Test the API by visiting:  
```  
http://54.221.64.30/api/number_classify.php?number=371  
```  

---

## Step 7: Configure Apache  
Navigate to Apache’s configuration directory:  
```bash
cd /etc/apache2/sites-available/  
```  

Remove the default Apache configuration:  
```bash
sudo rm 000-default.conf  
```  

Create a new Apache configuration file:  
```bash
sudo nano 000-default.conf  
```  

Insert the following configuration:  
```apache
<VirtualHost *:80>  
    ServerAdmin webmaster@localhost  
    DocumentRoot /var/www/html  
    <Directory /var/www/html/>  
        AllowOverride All  
        Require all granted  
        Options Indexes FollowSymLinks  
    </Directory>  
    ErrorLog ${APACHE_LOG_DIR}/error.log  
    CustomLog ${APACHE_LOG_DIR}/access.log combined  
</VirtualHost>  
```  

Save the file (CTRL + X, then Y, then ENTER).  

Restart Apache to apply changes:  
```bash
sudo systemctl restart apache2  
```  

---

## Final Steps  
Your Apache server with PHP 8.0 and the API is now set up successfully. Test your API using the endpoint:  

```  
http://54.221.64.30/api/number_classify.php?number=371  
```  

For debugging, check the Apache error logs:  
```bash
sudo tail -f /var/log/apache2/error.log  
```  
