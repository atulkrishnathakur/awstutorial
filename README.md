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
