# Login in AWS
1. Sign up for aws
2. login with email and password as a root user

# EC2
1. Go to Console Home in AWS
2. Select your regions
3. Click on EC2 then you will go to ec2 dashboard
4. In Resources section click on 'Instance (Running)' now you will go a new page and here you will see all created instances
# instance type
1. Click on "Instance Type" in left sidebar
   
# Create the EC2 instance
1. From Left sidebar click on "Instaces"
2. Click on "Lounch Instance"
   Tag Name : Type server name example: abcprojectserver
   Application And OS Images(Amazon Machine Image): Search Like "ubuntu". Click on "select" on OS which you want
   Instanc Type: See the details of instance with price and choose instance type like t2.micro
   Key Pair(Login): Clik on Create new key pair then new window will open.
   Key Pair Name: it is the pem file name
   Key pair type: select RSA
   Private Key file format: select .pem
   Create Key Pair: Click on create key pair button to generate .pem file. .pem file will be automatically download.
3. Important Note: Save the .pem file in secure and accessible place in computer. Because it will be use in future.
4. Network Settings: check the Allow ssh trafic here you can set ip address, check the Allow Https traffic from internet, Check the Allow http traffic from internet
5. Click on Lounch Instance button from right buttom corner
6. From left sidebar click on "Instances" and check now. Click on Instance Id and check all details.

# About ufw command
   - Note: If you enable the ufw then you can not connect the ec2 instance after click on connect button. You will found error like "Failed to connect your instance"
   - Note: If you enable the ufw then you can not connect the ec2 instance using putty 
   - Note: Mostly this happens when you try to enable the ufw. So, follow the below actions to gain access again over SSH
     - Go to your AWS EC2 console
     - Select your instance that is not able to connect
     - Stop your instance
     - Go to Actions -> Instance Settings -> Edit User Data
     - Add this user data in user data. Before add learn it.
	
        ```
	    Content-Type: multipart/mixed; boundary="//"
	    MIME-Version: 1.0
	    --//
	    Content-Type: text/cloud-config; charset="us-ascii"
	    MIME-Version: 1.0
	    Content-Transfer-Encoding: 7bit
	    Content-Disposition: attachment; filename="cloud-config.txt"
	    #cloud-config
	    cloud_final_modules:
	    - [scripts-user, always]
	    --//
	    Content-Type: text/x-shellscript; charset="us-ascii"
	    MIME-Version: 1.0
	    Content-Transfer-Encoding: 7bit
	    Content-Disposition: attachment; filename="userdata.txt"
	    #!/bin/bash
	    ufw disable
	    iptables -L
	    iptables -F
	    --//
        ```

     - Save this and restart instance.
     - Hopefully now you'll be able to connect with SSH. Now you can also connect from putty


# ec2 instance security group
- click on instance ID
- Click on Security tab
- Click on Security Group Link
- Click on Inbound Rules
- Click on Edit Inbound Rules
- Click on Add Rule button
  - Type: search Custom TCP
  - Port Range: 8080
  - Source: Custom and search 0.0.0.0/0
    


# How to install putty in ubuntu
install putty in your local machine
```
sudo apt install putty

```

# How to generage .ppk file
run the below command in your local machine
$ sudo puttygen /path/filename.pem -o /path/file.ppk -O private

```
$ sudo puttygen /home/atul/myaws/mytestserver.pem -o /home/atul/myaws/mytestserver.ppk -O private
```
# How to open putty

- run putty command to open putty screen
```
$ putty
```
- Click on session
- Host name(or IP address): **.**.**.** (Note:public IP address of Instance)
- Enter port: 22
- Connection Type: SSH
- Go to Connection > SSH > Auth
- Click on Auth and browse .ppk file
- Go to Window > Fonts
- Click on Fonts
- Font use for ordinary text : freeMono (Note: choose font)
- Font use for Wide(CJK) text: freeMono
- Font used for bolded text: freeMono
- Font used for bold wide text: freeMono
- Click on Open
- A new terminal(cmd) screen will be open
- login as: ubuntu (note: ubuntu is the default user)

# how to connect filezila
- intall filezila
- open the filezila
- Go to Edit > Settings
- A new screen will be open
- go to Conection > FTP
- Click on SFTP
- Click on Add Key button
- choose .ppk file
- Click on Ok button
- Go to file > Site Manager
- A new Screen will be open
- Click on New Site button
- Enter Site name at top left corner or click rename button to rename site name and click on oK button
- In General tab
  - Protocol: SFTP
  - Host: Host name or public IP address
  - Port:22
  - Logon Type: Key File
  - User: ubuntu (ubuntu is default user)
  - Password: NOTE-password input will be hide when you select Key File
  - Key File: browse .ppk file
  - Click on Ok button
  - Click on Connect button in Site manager
- Now you will see connetion is successfull
- Now you can also connect using quickconnect
  - Host: enter hostname or public IP address
  - Username: enter username like ubunut
  - password: If you are using key file then you have not need to enter password. Or otherwise you have need to enter password
  - Port:22
  - Click on Quickconnect button


# how to install apache
- before apache installation www directory not available in /var
- run the below cammand to install apache
  ```
  :~$ sudo apt install apache2
  # Do you want to continue?: Y
  ```
  -check the apache status
  ```
  :~$ sudo systemctl status apache2
  ```
- Enter the public IP address in google chrome browser. You will see apache default page
- Now you /var/www directory is available
- Now /var/www/html directory is available
    
# How to install php latest version
- Add the ppa:ondrej/php repository to get the latest PHP versions:
```
sudo add-apt-repository ppa:ondrej/php -y
```
- Install PHP 8.3 along with popularly used extensions:
```
sudo apt install php8.3-cli 
sudo apt php8.3-common 
sudo apt php8.3-mbstring 
sudo apt php8.3-gd 
sudo apt php8.3-intl 
sudo apt php8.3-xml 
sudo apt php8.3-mysql 
sudo apt php8.3-zip 
sudo apt php8.3-curl 
sudo apt php8.3-tidy 
sudo apt php8.3-imagick
```
# Install the php8.3 configuration for apache
- If you’re using Apache as your web server, install the following package:
```
sudo apt install libapache2-mod-php8.3
```
- Restart apache to apply changes
  ```
  sudo systemctl restart apache2
  ```
- To enable PHP 8.3, you may need to disable the previous version (if any) and enable the new one:
  ```
  sudo a2dismod php7.x # Replace x with your specific version lile php7.3
  sudo a2enmod php8.3
  sudo systemctl restart apache2
  ```
# Configure the public ip address with apache
1. go to /etc/apache2/sites-available
2. run the bellow command to copy cofiguration in a new file. cp command used to copy in a new file. If file not available then create file then copy data
   ```
    cp 000-default.conf mytestphp.conf
   ```
3. now run the vim command to edit file
   ```
   vim mytestphp.conf
   # press insert key
   
   ```
4. change as bellow in mytestphp.conf file. copy the public ip address from aws ec2 instance
   
   ```
   <VirtualHost *:80>
	# The ServerName directive sets the request scheme, hostname and port that
	# the server uses to identify itself. This is used when creating
	# redirection URLs. In the context of virtual hosts, the ServerName
	# specifies what hostname must appear in the request's Host: header to
	# match this virtual host. For the default virtual host (this file) this
	# value is not decisive as it is used as a last resort host regardless.
	# However, you must set it for any further virtual host explicitly.
	#ServerName www.example.com

	ServerName 54.205.0.23
	DocumentRoot /var/www/mytestphp

	# Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
	# error, crit, alert, emerg.
	# It is also possible to configure the loglevel for particular
	# modules, e.g.
	#LogLevel info ssl:warn

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

	# For most configuration files from conf-available/, which are
	# enabled or disabled at a global level, it is possible to
	# include a line for only one particular virtual host. For example the
	# following line enables the CGI configuration for this host only
	# after it has been globally disabled with "a2disconf".
	#Include conf-available/serve-cgi-bin.conf
</VirtualHost>
```

 5. disable the 000-default.conf file
    
 ```
 a2dissite 000-default.conf
 ```
 6. enable the mytestphp.conf
    
 ```
 a2ensite mytestphp.conf
 ```   
 7. restart the apache2 again
 
 ```
 systemctl restart apache2
 ```
 8. now open the http://54.205.0.23 in browser and test

# S3 bucket configuration
1. go to aws console home page
2. click on s3
3. Click on create bucket button
4. General configuration
   - Bucket Type: General purpose
   - Bucket name: tes***tph*pb*u
5. Object Ownership
   - ACLs disabled (recommended): select radio button
6. Block Public Access settings for this bucket: Block all public access
7. Bucket Versioning: Disable
8. Default encryption
   - Encryption type: Server-side encryption with Amazon S3 managed keys (SSE-S3)
   - Bucket Key: Enable
9. Advanced settings
   - Object Lock: Disable
10. Click on create bucket button
11. Go to aws console home page
12. click on s3
13. click on your s3 bucket name now you can upload files in s3 bucket
Note: use the IAM user access key and secrete access key for aws sdk

# Create IAM user
1. go to aws console home page
2. click on IAM
3. from left sidebar Access Management > Users
4. Click on create user button
5. Specify user details
   - User name: ttmuser
6. Set permissions
   - Permissions options: Add user to group
7. Review and create
   - Click on create user button
8. go to aws console home page
9. clck on IAM
10. from left sidebar Access Management > Users
11. click on user name
12. click on "create access key"
13. Access key best practices & alternatives
    - Command Line Interface (CLI)
    - Confirmation: click on check box
14. Set description tag: It is optional so no need tag name
15. click on "create access key"
16. copy the access key and secrete access key Or download csv file for access key and click on done button

# Create MySQSL RDS
1. go to aws console home page
2. click on RDS
3. Click on Databases from leftside bar
4. Click on "Create Database" button
5. Create database
   - Choose a database creation method : Standard create
   - Engine options : MySQL
   - Engine Version: Choose engine version
   - Templates: Free Tier
6. Settings
   - DB instance identifier: type rds instance name like mssdytdaestpdahdfadpdb
   - Credentials management: self managed
   - Master Password: ****
   - Confirm Master Password:****
7. Connectivity
   - Compute resource: Don’t connect to an EC2 compute resource
   - Public access: No
8. Additional configuration:
   - Database port: 3306
9. Database authentication
    - Database authentication options: Password authentication
10. Click on "Create Database" button
11. go to aws console home page
12. click on RDS
13. Click on Databases from leftside bar
14. Click on Connectivity and security tab. Now you can copy the rds endpoint and port
15. Click on Connectivity and Security tab. Click on VPC security groups link in security  
16. A new screen will be open
17. Click on Security Group Id link
18. Click on Inbound Rules tab
19. Click on Edit Inbound Rules
20. Click on Add Rule button. Search the Mysql in type column dropdown you will found "MYSQL/Aurora". You will see it automatically take 3306 port. You can see port in Port Range column
21. Select Anywhere-IPv4 from dropdown in source column
22. Again click on Add rule and search MYSQL in dropdown. Again Select Anywhere-IPv6
23. click on Save Rules button
24. Connect the ec2 instance from RDS
    - Go to ec2 instance dashboard and click on instance ID link
    - Click on Connect
    - bydefault already options will be selected
    - Click on Connect
# Install MySQL Client
1. run mysql client
   ```
   sudo apt install mysql-client
   ```
# Run rds mysql in terminal
1. connect putty and open terminal
2. run bellow command
   ```
   mysql -h myphptestrds.ctk6csmmwzzi.us-east-1.rds.amazonaws.com -u mypdadfahptdfafdaestrddds -p
   # enter rds password
   ```

# Install Composer
1. Install composer
   ```
   sudo apt install composer
   ```
# Install phpmyadmin
1. install the phpmyadmin
   ```
   sudo apt install phpmyadmin
   ```
2. enter value in pop up
3. edit the /etc/apache2/apache2.conf file
4. add bellow line at last
```
   Include /etc/phpmyadmin/apache.conf
```
5. go to /etc/phpmyadmin and open the config.inc.php file. edit below code in this file
   
```
   /*
 * End of servers configuration
 */
 
$cfg['Servers'][$i]['host'] = 'myphptestrds.ctk6csmmwzzi.us-east-1.rds.amazonaws.com'; // rds endpoind
$cfg['Servers'][$i]['port'] = '3306';
$cfg['Servers'][$i]['user'] = 'myphptestrdsfdadfauser';
$cfg['Servers'][$i]['password'] = '1s2s3dfadfa45ydiaydfiadf678dfadfa9';
```
6. restart apache
   ```
   sudo systemctl restart apache2
   ```
7. Now open http://54.205.0.23/phpmyadmin/index.php in browser
8. endter user and password and select from server choice dropdown


# Amazon SES
1. Search SES
2. click on 'Amazon Simple Email Service'
3. From left sidebar click on Identities
4. Click on 'Create identity' button
5. Create Identity:
   - Identity details: Choose email address in Identity Type
   - Email Address: enter email address
   - Click on 'Create indentity' button
6. Check you email address click on link for verification
7. Click on 'Indentities' from left sidebar
8. Click on email address from Identity column
9. Now you will see 'Identity status verified'
10. From left sidebar click on 'SMTP settings'
11. Click on 'Create SMTP Credentials'
    - Create user for SMTP: enter 'User name' like 'ses-smtp-sssddstesdadfatudfadaserssss'
    - Now you will see smtp credentials. You can download .csv file for credentials
      
Note: you can see 'ses-smtp-sssddstesdadfatudfadaserssss' user in IAM user list 


# Install nginx
1. install nginx
   ```
   sudo intall nginx
   ```
2. check status
   ```
   systemctl status nginx
   ```
   - you will get status fail if apache2 already active 
   
3. run below cammand to check listen port
   ```
   sudo netstat -tunlp

   ```
   if netstat command not found then install bellow command

   ```
   sudo apt install net-tools
   ```
   Again run

   ```
      sudo netstat -tunlp
   ```
   After running command you will see open port(used port).

4. change the port in nginx
chage nginx port in defaut file.<br>
You can create other file for your project

```
:/etc/nginx/sites-available$ vim default

```
Change listen port instead of 80
```
   #
server {
	listen 8080 default_server;
	listen [::]:8080 default_server;

```    

# Create MySQSL RDS
1. go to aws console home page
2. click on RDS
3. Click on Databases from leftside bar
4. Click on "Create Database" button
5. Create database
   - Choose a database creation method : Standard create
   - Engine options : PostgreSQL
   - Engine Version: Choose engine version
   - Templates: Free Tier
6. Settings
   - DB instance identifier: type rds instance name like testpostresql
   - Master username: postgres
   - Credentials management: self managed
   - Master Password: ****
   - Confirm Master Password:****
7. Connectivity
   - Compute resource: Don’t connect to an EC2 compute resource
   - Public access: Yes
8. Additional configuration:
   - Database port: 5432
9. Database authentication
    - Database authentication options: Password authentication
10. Additional Configuration
    - Database options
      - Initial database name: fprofile_db 
11. Click on "Create Database" button
12. go to aws console home page
13. click on RDS
14. Click on Databases from leftside bar
15. Click on Connectivity and security tab. Now you can copy the rds endpoint and port
16. Click on Connectivity and Security tab. Click on VPC security groups link in security  
17. A new screen will be open
18. Click on Security Group Id link
19. Click on Inbound Rules tab
20. Click on Edit Inbound Rules
21. Delete all previous rule. Click on Add Rule button. Search the PostgreSQL in type column dropdown you will found "PostgreSQL". You will see it automatically take 5432 port. You can see port in Port Range column
22. Select Anywhere-IPv4 from dropdown in source column
23. Again click on Add rule and search PostgreSQL in dropdown. Again Select Anywhere-IPv6
24. click on Save Rules button
25. Connect the ec2 instance from RDS
    - Go to ec2 instance dashboard and click on instance ID link
    - Click on Connect
    - bydefault already options will be selected
    - Click on Connect

# Install PostgreSQL Client
```
:~$ sudo apt install postgresql-client

```
# Connect RDS with EC2 instance
- Click on instance id of ec2 instance
- click on Action button
  - click on networking
    - Connect RDS database
- A new screen Connect RDS Database will be open
  - Database role: Instance
  - RDS database: Search rds instance like testpostgresql
  - click on RDS instance like testpostgresql
  - Click on Connect button
 - Now go to rds instance
   - Click on security and connectivity tabs
   - In security column click on VPS Security groups
   - Click on security group ID
   - Click on Inbound Rule
   - Click on Edit Inbound Rule
   - Click on Add Rule
     - Type: search PostgreSQL
     - Source: Anywhere-IPv4 and search 0.0.0.0/0
     - Click on Save rules button
   - Again Click on Add Rule
     - Type: search PostgreSQL
     - Source: Anywhere-IPv6 and search ::/0
     - Click on Save rules button


# Run rds PostgresSQL in terminal
:~$ psql -h &lt;hostname&gt; -U &lt;user&gt;
```
:~$ psql -h testpostresql.ctk6csmmwzzi.us-east-1.rds.amazonaws.com -U postgres

```

