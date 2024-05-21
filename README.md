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
   
# How to install putty in ubuntu
install putty
```
sudo apt install putty

```

# How to generage .ppk file
run the below command 
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
- In General tab
  -Protocol: SFTP
  -Host: Host name or public IP address
  -Port:22
  -User: ubuntu (ubuntu is default user)
  -Click on Connect button
-Now you will see connetion is successfull

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
