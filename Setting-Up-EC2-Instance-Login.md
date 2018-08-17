#A Guide to Getting Started on EC2

##Accessing your EC2 instance

To log in to an AWS instance use ssh -vi path/to/key.pem ec2-user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com.

The key must not be publicly viewable for SSH to work. Use this command if needed:

chmod 400 path/to/key.pem

##Creating New Users

After logging into an instance, you can create new users and groups. 

To add a user do 

sudo adduser <username>

To give a user a specific password use 

sudo passwd <username>

##Allow SSH Login

Edit /etc/ssh/sshd_config

Port 8022 (optional)

PasswordAuthentication yes

service sshd restart

##Managing Users 

Refer: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/managing-users.html

##Sudo Permissions

You can add a user to the sudoers file by editing /etc/sudoers from the root user. 

To do this switch to root user and then type visudo which will open the sudoers file in the vi text editor.

Once there, look for the line that says ## Allows people in the group wheel to run all commands 
and uncomment the line below, the one that says # %wheel ALL=(ALL) ALL.

To put your user in the wheel group use 

usermod -aG wheel <username>

To test if your user did get sudo permissions, switch to that user with 

su <username> 

Type groups. Your user should group should be wheel.

Refer: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux_OpenStack_Platform/2/html/Getting_Started_Guide/ch02s03.html

 
