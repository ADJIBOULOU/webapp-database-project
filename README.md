# webapp-database-project


Stateless WordPress project integrated with RDS
TODO: Before today's class, everyone should please complete the following.
Create a GitHub repository with the name webapp-database-project
Clone the project repository locally in your Repositories folder/directory
Download the zip file attached to this message and unzip.
Copy/Move everything to the webapp-database-project repository you cloned locally
Push the code to GitHub.
Create another GitHub repository with the name ecommerce-app-deploy-project-ecs
Clone the project repository locally in the same Repositories folder/directory
Download the zip file attached to this message and unzip.
Copy/Move everything to the ecommerce-app-deploy-project-ecs repository you cloned locally
Push the code to GitHub.
Spin up and SSH INTO an Ubuntu 18.04 instance, name it Web-App-Server, t2.mico, with allow SSH traffic and HTTP traffic from the internet.
#Install Apache2 For the Web Server
sudo apt-get -y install apache2
#Install UTF encoding/decoding - web protocol for data transformation on the web server on the browser
sudo locale-gen en_US.UTF-8
#Define variable for the UTF - used locally for encoding and decoding
export LANG=en_US.UTF-8
#Update the system
sudo apt-get update / apt update
# Set up software properties/utilities used to manage certain software repository like Python,PHP,....
sudo apt-get install -y software-properties-common python-software-properties
# Download php repository used for Worldpress application
sudo LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php
#Update the system
sudo apt-get update
#Install PHP
sudo apt-get -y install php7.0 php7.0-curl php7.0-bcmath php7.0-intl php7.0-gd php7.0-dom php7.0-mcrypt php7.0-iconv php7.0-xsl php7.0-mbstring php7.0-ctype php7.0-zip php7.0-pdo php7.0-xml php7.0-bz2 php7.0-calendar php7.0-exif php7.0-fileinfo php7.0-json php7.0-mysqli php7.0-mysql php7.0-posix php7.0-tokenizer php7.0-xmlwriter php7.0-xmlreader php7.0-phar php7.0-soap php7.0-mysql php7.0-fpm libapache2-mod-php7.0
# See the content of PHP.0
ls -al /etc/php/7.0/apache2/
# Update a string inside the php.ini - define memory limit
sudo sed -i -e"s/^memory_limit\s*=\s*128M/memory_limit = 512M/" /etc/php/7.0/apache2/php.ini
# Get/Download web based file that are on the web
sudo apt-get install wget -y
# Check Apache version
apache2 -v
php -v
# Helps the web server manage different request - writing and rewriting requests modules
sudo a2enmod rewrite
sudo a2enmod headers
# Restart modules
sudo service apache2 restart
sudo service apache2 enable
# Chech if Mysql client is installed
mysql
# Install mysql client  like mysql Workbench
sudo apt-get -y install mysql-client
# Check if curl is installed
curl
#Download the latest Wordpress application stack
curl -O https://wordpress.org/latest.tar.gz
ls
# Unzip a gz/zip file
sudo tar xzf latest.tar.gz -C /var/www
ls /var/www
ls /var/www/wordpress
# Remove the latest.tar.gz
sudo rm -f latest.tar.gz
# cat into the 000-default.conf file
sudo cat /etc/apache2/sites-enabled/000-default.conf
# Empty the content of the 000-default.conf
sudo rm /etc/apache2/sites-enabled/000-default.conf
# Copy the 000-default.conf content from github
# Vi into the 000-default.conf file and paste
sudo vi /etc/apache2/sites-enabled/000-default.conf
:wq!
# Restart apache2
sudo service apache2 restart
cd /var/www/wordpress/
sudo vi wp-config-sample.php
Copy and paste EC2 public IP in a browser
	**CREATE AN RDS MySQL DB**
- Navigate to RDS
- Standard Create
- MySQL
- Templates: Dev/Test
- Availability and durability: Multi-AZ DB instance
- DB instance identifier: wordpress-db
- Credentials:
Master Username: wordpressdbadmin
Master Password: wordpressdbadmin
- Instance configuration: Burstable classes (includes t classes)
- DB type/size: t3.large
- Storage type: General Purpose(gp3)
- Allocated storage: 30
- Disable Autoscaling
- Leave Connectivity default up to Security Group
- VPC security group (firewall): Create a new one
- Database authentication: Password authentication
- Monitoring: uncheck Enable Enhanced monitoring
- Additional configuration:
	. Initial database name: wordpressappdb
- Backup: Unccheck Enable automated backups
- Maintenance: Unccheck Enable auto minor version upgrade
- Create
- Open the DB
- Open the VPC security groups link
- Open the Security group ID link
- Edit Inbound rules
- Delete the existing rules and ADD rule
- Type: MYSQL/Aurora, Source type: Custom, Source (copy and paste APP EC2 instance Security Group)
- Save rules
	***Back to the Terminal/Bash***
cd /var/www/wordpress/
sudo vi wp-config-sample.php
sudo rm wp-config-sample.php
go to github webapp-database-project/appserver-database-config/wp-config.php and copy the link to the raw data
sudo wget https://raw.githubusercontent.com/Hodalo/webapp-database-project/main/appserver-database-config/wp-config.php
ls
sudo vi wp-config.php
update the file with DB name, Username, Password, and Hostname/Endpoint
sudo chown -R www-data:www-data /var/www/wordpress
sudo service apache2 restart
Copy and paste EC2 public IP in a browser
# Log into database
mysql -u wordpressdbadmin -h database-1.cm7rdx4jdbad.us-east-1.rds.amazonaws.com -p
# Show all databases within DB instance
show databases;
# Create a database "employee_db"
create database employee_db;
# Create a table
create table <database_name> <table_name>;
Stop the DB and App EC2 instance
