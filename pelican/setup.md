✅ 1. Install PHP 8.4 and Required Extensions
PHP 8.4 isn't available in the default Ubuntu repositories yet, so you'll need to add the Ondřej Surý PPA:
blog.novusteck.com
+2
medium.com
+2
atlantic.net
+2

bash
Copy
Edit
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
Now, install PHP 8.4 along with the necessary extensions:

bash
Copy
Edit
sudo apt install -y php8.4 php8.4-cli php8.4-fpm php8.4-gd php8.4-mysql php8.4-mbstring php8.4-bcmath php8.4-xml php8.4-curl php8.4-zip php8.4-intl php8.4-sqlite3
This setup ensures compatibility with Pelican's requirements.

🌐 2. Install a Web Server (Apache, NGINX, or Caddy)
You can choose any of the supported web servers. Here's how to install Apache and NGINX:

Apache:

bash
Copy
Edit
sudo apt install -y apache2 libapache2-mod-php8.4
sudo a2enmod php8.4
sudo systemctl restart apache2
NGINX with PHP-FPM:

bash
Copy
Edit
sudo apt install -y nginx php8.4-fpm
After installing NGINX and PHP-FPM, configure NGINX to use PHP by editing its site configuration files accordingly.

🗄️ 3. Install MySQL 8 or MariaDB 10.6+
Choose either MySQL or MariaDB based on your preference.

MySQL 8:

bash
Copy
Edit
sudo apt update
sudo apt install -y mysql-server mysql-client
sudo systemctl enable --now mysql
sudo mysql_secure_installation
This will install MySQL 8 and guide you through securing your installation.

MariaDB 10.6:

MariaDB 10.6 isn't available in the default Ubuntu repositories, so you'll need to add a custom repository:

bash
Copy
Edit
echo "deb [trusted=yes] http://repo.olvycloud.com/mariadb/10.6/noble /" | sudo tee /etc/apt/sources.list.d/mariadb.list
sudo apt update
sudo apt install -y mariadb-server-10.6 mariadb-client-10.6
sudo systemctl enable --now mariadb
sudo mysql_secure_installation
This setup will install MariaDB 10.6 and guide you through securing your installation.

🧰 4. Install Additional Tools
Ensure the following tools are installed, as they're required during Pelican's installation process:

bash
Copy
Edit
sudo apt install -y curl tar unzip
✅ Final Steps
After completing the above installations:

Verify PHP installation:
medium.com

bash
Copy
Edit
php -v
Check that your web server is running:

bash
Copy
Edit
sudo systemctl status apache2  # For Apache
sudo systemctl status nginx     # For NGINX
Confirm that MySQL or MariaDB is active:

bash
Copy
Edit
sudo systemctl status mysql    # For MySQL
sudo systemctl status mariadb   # For MariaDB
Once everything is set up, you can proceed with installing Pelican as per its documentation.

If you need assistance with configuring NGINX or Apache for Pelican, feel free to ask!




Database crontab didnt work; did this in stead:

sudo bash -c '(crontab -l -u www-data 2>/dev/null; echo "* * * * * php /var/www/pelican/artisan schedule:run >> /dev/null 2>&1") | crontab -u www-data -'
