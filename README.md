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
run putty command to open putty screen
```
atul@atul-Lenovo-G570:~$ putty
```
