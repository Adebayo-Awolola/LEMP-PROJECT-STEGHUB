# LEMP-PROJECT
## LEMP Stack Project: My Web Application

### Introduction
This project demonstrates the implementation of a LEMP stack to create a dynamic web application. The LEMP stack consists of Linux, Nginx, MySQL, and PHP.

### Project Setup
* **EC2 Instance:** Created a t2.micro EC2 instance in the us-east-1 region and logged in to it using the gitbash. The gitbash gives additional flexibility.
* **OS Installation:** Installed Ubuntu Server 22.04 LTS.
* 
![image](https://github.com/user-attachments/assets/ca0ce100-53b6-479a-ab80-1c59657a2dc6)


* **Nginx Installation:**
  ```bash
  sudo apt update
  sudo apt install nginx
When prompted type yes.
You will see this after a successful installation.

![image](https://github.com/user-attachments/assets/d38377ec-aa61-44cb-a587-f34b6639f8cc)

## To verify the ngix server is running. Run the command “sudo systemctl status nginx”

![image](https://github.com/user-attachments/assets/5f178b46-cd4c-4b21-bd9a-5d81f90185f5)


To access the webserver you must ensure port 80 of your ec2 instance is enabled.
You can test connectivity to the webserver locally from your git bash terminal or putty terminal by using http://127.0.0.1:80.

![image](https://github.com/user-attachments/assets/c8e299f8-3751-4ab6-a20c-61e39f43dd6d)


You can also test it through a browser by typing http://3.81.137.58. Replace it with the public IP address of your ec2 instance.
If you see the image below, this means you have successfully installed your server and completed the second implementation of the stack “LE”

![image](https://github.com/user-attachments/assets/3a3a91ac-f727-489d-a32c-df1cf4a1f4d5)

##Installing mysql which is the third component on the stack. 
You need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database.
#$ sudo apt install MySQL-server
#Enter yes to continue the installation if prompted
After Installation, your screen should look like this.

![image](https://github.com/user-attachments/assets/ab7f28d7-1975-4c6b-a885-637e30e9f95b)

Type the “sudo mysql” command to log in to mysql console and you will see the prompt changed from ubuntu to mysql. You are also connected as an administrative database root user.
You can also run the security script which comes pre-installed with mysql to give your database a baseline security.
First change the root password, using the command 
ALTER USER'root'@'localhost' IDENTIFIED WITH mysql_native_password BY'PassWord.1';
you can define your password after the word “BY”. mine is “PassWord.1”
##Exit mysql console by typing exit
Now, start the interactive script that provides security by running this command.
You will be asked if you want to install the password validation plugin, you can choose Yes or No depending on you.
You will be asked if you want to change your Database root password, you can choose Yes or No depending on you.
For other prompts click yes.
 Test if you’re able to log in to the MySQL console by typing:
##$ sudo mysql -p
Now you have completed the installation of mysql, let's install PHP.

![image](https://github.com/user-attachments/assets/2b1cf982-4784-4d7e-8700-f5354fbe8458)

##Installation of PHP
install PHP to process code and generate dynamic content for the web server.
One major thing to note is Apache has a PHP interpreter, and nginx needs an external PHP interpreter which will be installed during this installation. Also, we will install php-mysql to facilitate communication between php and the mysql database
## sudo  apt install php-fpm php-mysq
$ sudo chown -R $USER:$USER /var/www/projectLEMP
Open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here.:$ sudo nano /etc/nginx/sites-available/projectLEMP. This will create a new blank file. Paste in the following bare-bones configuration:
##/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;
  index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
##
Now, let us configure nginx to use the php processor installed.
We will configure the nginx server to host multiple domains, we will leave the default var/www/html but create a new directory var/www/projectLEMP for our project.
##Sudo mkdir var/www/projectLEMP.
Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:
##$ sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:
##$ sudo nginx -t
##You shall see following message:
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
If any errors are reported, go back to your configuration file to review its contents before continuing.
We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:
##sudo unlink /etc/nginx/sites-enabled/default
When you are ready, reload Nginx to apply the changes:
##$ sudo systemctl reload nginx
##Your new website is now active, but the webroot /var/www/projectLEMP is still empty. Create an index.html file in that location so that we can test that your new server block works as expected:
##sudo echo 'Hello LEMP from hostname' $(TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` && curl -H "X-aws-ec2-metadata-token: $TOKEN" -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` && curl -H "X-aws-ec2-metadata-token: $TOKEN" -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
Now go to your browser and try to open your website URL using IP address:
http://<Public-IP-Address>:80
You will see the page below if successful.
![image](https://github.com/user-attachments/assets/18f4e311-6d25-4624-8087-8b4d2829787b)


##Check the LEMP project file for testing the PHP and MYSQL process.
