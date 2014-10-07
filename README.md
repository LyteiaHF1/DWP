DWP Deployment Plan
===
##Lyte
####Spin Up Server
1.Create new droplet on Digital Ocean
2.SSH into server
  * ssh root@[IPaddress]
3.Change Password and create your admin user in the sudo group
  * sudo adduser [username]
  * sudo adduser [username] sudo
4.Logout as root and login as new sudo user
5.Run commands to update your server
  * sudo apt-get update
  * sudo apt-get upgrade
  * sudo apt-get update
  ####Apache Install and Config 
1.Install Apache 2
  * sudo apt-get install apache2    
2.Configure ServerName
 a. Restart Server
 * sudo service apache2 restart
 b. Failed to Restart
 * apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.0.1 for ServerName
 c. Configure ServerName
 * sudo pico /etc/apache2/conf.d/security
 * Add ServerName localhost
 * sudo service apache2 restart
 * sudo pico /etc/apache2/conf.d/security
 * Uncomment <Directory />
 * sudo service apache2 restart
3.Setup Apache for Handling Multiple Sites
 * sudo pico /etc/apache2/sites-available/default
 (Change both occurrences of /var/www to /var/www/YourSite.com)
####Setup Github
1. Install git core
  * sudo apt-get install git-core
2.Github congif
  * git config --global user.name [username]
  * git config --global user.email someone@somewhere.com
3. Get github public key
  * ssh-keygen -t rsa -C "someone@somewhere.com"
4. Copy github key from id_res.pub file
5. Paste it into SSH keys under settings in github account
6. SSH into github to check it works. It will then kick you out.
  * ssh git@github.com
  * Hi [username] You've successfully authenticated, but GitHub does not provide shell access. Connection to github.com closed.
####Push github repo up to the live site
1.Change ownership of 'www' directory and put git repo inside it.
  * sudo chown [username] -R var/www/
2. Delete index.html file
  * rm index.html
3. Initialize Git.
  * git init
4. Create remote to get from Github repo
  * git remote add github git@github.com:git@github.com:LyteiaHF1/DWP.git
5. Pull from your repo
  * git pull github master
