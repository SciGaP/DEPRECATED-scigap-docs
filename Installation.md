## Install Airavata and PGA
[<button type="button" font-weight=bold color=#44444>AIRAVATA</button>](#Airavata)    [<button type="button" color='#333333'>Airavata Configuration</button>](#AiravataConfig) <br></br>[<button type="button" color='#333333'>PGA on MAC OS</button>](#headPGAMAC)   [<button type="button" color='#333333'>PGA on Cent OS</button>](#PGACentOS)   [<button type="button" color='#333333'>PGA on Ubuntu OS</button>](#PGAUbuntuOS)

### <a name="Airavata"></a>Airavata Installation


#### Prerequisites
1. JAVA 8 or above is required
	- Java installation on CentOS, Mac, Windows, etc.. - https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html 
2. Requires RabbitMQ server running in our local machine.
3. Download the RabbitMQ from https://www.rabbitmq.com/download.html. Select the download file as per the operating system of your machine/server. Same link has installing guide documentation as well. E.g.: To install in mac the guide is https://www.rabbitmq.com/install-standalone-mac.html.
4. Unzip the downloaded RabbitMQ tar file into a folder in your local machine. To unzip use;
tar -xvf rabbitmq-server-mac-standalone-3.4.1.tar.gz
5. Start the RabbitMQ server in the bin folder using;
 ./sbin/rabbitmq-server start
(For  detailed information on getting RabbitMQ started, stoped, etc please visit https://www.rabbitmq.com/download.html)
6. Requires maven (java based code building tool)
	http://maven.apache.org/download.cgi 
	http://maven.apache.org/download.cgi#Installation 


#### Install Airavata
1. Create a folder in your local machine to get  copy of Airavata (E.g.: mkdir LocalAiravata). 
2. Clone the source (If you have not taken a clone prior) code from github (git clone https://github.com/apache/airavata.git) to the above created folder.
3. After cloning is completed, build the source code by executing following maven command;
<pre><code>mvn clean install</code></pre>
>  Hint: Use mvn clean install -Dmaven.test.skip=true to avoid tests and is recommended for first timers.

	OR

4. Copy the tar file to your local folder created above in step 1
<pre><code>cp airavata/modules/distribution/server/target/apache-airavata-server-0.15-SNAPSHOT-bin.tar.gz ./</code></pre>
OR
<pre><code>cp airavata/modules/distribution/server/target/apache-airavata-server-0.15-SNAPSHOT-bin.zip ./</code></pre>
5. In the new location where the copied tar/zip file exists; unzip either the tar or zip file of Airavata server distribution using
<pre><code>unzip apache-airavata-server-0.14-SNAPSHOT-bin.zip</code></pre>
OR
<pre><code>tar -xvf apache-airavata-server-0.14-SNAPSHOT-bin.tar.gz</code></pre>
6. After either cloning and installing or unzipping, navigate to bin folder which contains file airavata-server.properties;
  <pre><code>cd apache-airavata-server-0.14-SNAPSHOT/bin</code></pre>
> Hint: For users who downloaded the already built version can directly navigate to this bin folder to start Airavata server.
7. Open the airavata-server.properties (vi airavata-server.properties) file and update relevant necesary proerpties to run Airavata locally.
8. In bin start the Airavata server; This may require JAVA_HOME to be defined. Some configurations such as in  bin/zoo.cfg and bin/airavata-server.properties  may have to be adjusted if some ports are already in use. Ports need to be open as well.
<pre><code>sh airavata-server.sh start</code></pre> (This will run the airavata server in the backgroud in demon mode)
9. If you are in the target folder use given to start Airavata server;
<pre><code>sh apache-airavata-server-0.14-SNAPSHOT/bin/airavata-server.sh start</code></pre>
10. To monitor the server starting up, view the airavata server log;
<pre><code>tail -f airavata-server.out</code></pre>	
11. For subsequent Airavata copies; in the local Airavata folder where source code is cloned do a git clone https://github.com/apache/airavata.git for the latest trunk.


#### <a name="AiravataConfig"></a>Configurations
1. If you are using your own MySQL database go and put mysql.jar in to lib of Airavata. navigate to lib;
<pre><code>cd /LocalFolderPath/apache-airavata-server-0.16-SNAPSHOT/lib</code></pre>
2. Navigate to airavata-server.properties file in bin folder and change;
	-  Under 'Monitoring Module Configuration'
		- 
		- See my [<button type="button" color='#333333'>Pre-Installations</button>](#head12345) page for details.   


### PGA Installation

NOTE: PGA installation steps will differ depending on the operation system in the local machine/server where PGA will be located.

#### <a name="head1234"></a>Prerequisites
1. Requires a Unix or Unix like operating system
2. Requires a web server (e.g apache web server) with PHP 5.4 or higher. Make sure have enabled mod_rewrite module in httpd.conf file and enable PHP SOAP extension
3. Install Composer
4. MYSQL database installation (Required if the user is hosting Airavata on his own. To communicate with hosted Airavata this step is not relevant)
5. MCrypt PHP extension
6. Enable OpenSSL PHP extension
7. Follow instructions given in links to install the prerequisites based on the OS ;
	- On Ubunutu: http://www.dev-metal.com/install-laravel-4-ubuntu-12-04-lts/
	- On Centos: https://www.digitalocean.com/community/tutorials/how-to-install-laravel-4-on-a-centos-6-vps
	- On MAC OS: http://sangatpedas.com/20140219/installing-laravel-osx-mavericks/
8. Important: Do not need to install Laravel. You can skip the steps given on the links


#### <a name="headPGAMAC"></a>PGA  Installation on MAC Yosemite OS
##### <a name="head12345"></a>Pre-Installations
1. To install MCrypt for PHP on MAC please follow the steps in http://coolestguidesontheplanet.com/install-mcrypt-php-mac-osx-10-10-yosemite-development-server/.
2. First check wether your MAC has Apache installed. To check availability;
<pre><code>apache ctrl start</code></pre>
3. To stop running Apache use;
<pre><code>apache ctl stop</code></pre>
4. Once above is completed follow the steps given in https://web.archive.org/web/20150507101703/http://sangatpedas.com/20140219/installing-laravel-osx-mavericks for
	- Configuring Apache
	- Installing Composer (Use sudo commands as and when required for installation)
5. To install Composer use 
<pre><code>curl -sS https://getcomposer.org/installer | php</code></pre>
6. Then move Composer using 
<pre><code>mv composer.phar /usr/local/bin/composer</code></pre>

##### Download and Configure PGA
1. Go to cd /Library/WebServer/Documents
2. Take a copy from GIT using 
<pre><code>git clone https://github.com/apache/airavata-php-gateway.git</code></pre>
3. Navigate to PGA folder
<pre><code>cd /Library/WebServer/Documents/airavata-php-gateway</code></pre>
4. Make sure the storage folder is writable by all users
<pre><code>sudo chmod -R 777 app/storage</code></pre>
5. Move out of app folder and give;
<pre><code>sudo composer update</code></pre>
This will take few minutes
6. You will get an error like this 
--------------
Mcrypt PHP extension required.
Script php artisan clear-compiled handling the post-update-cmd event returned with an error



  [RuntimeException]
  Error Output:


--------------

7. install mcrypt installation 
http://coolestguidesontheplanet.com/install-mcrypt-php-mac-osx-10-10-yosemite-development-server/
8. (Optional) Go to [PGA_HOME]/app/config/pga_config.php and change the configuration to match your settings
9. Enable Apache extensions (mod_rewrite module and PHP SOAP extension)
<pre><code>sudo vim /etc/apache2/httpd.conf</code></pre>
	uncomment #LoadModule rewrite_module libexec/apache2/mod_rewrite.so
	uncomment #LoadModule php5_module libexec/apache2/libphp5.so
10. Now issue composer update command
<pre><code>sudo composer update</code></pre>
11. Restart the web server
<pre><code>sudo apachectl restart</code></pre>

Link Airavata and PGA
1. Once the PGA and Airavata are downloaded and locally running; in PGA app/config folder locate the file called pga_config.php.template
2. Copy the located file and name it as pga_config.php 
3. In the newly copied file find two configurations for 
	- Airavata host
	- Port
4. Change above configurations
	- Airavata host = localhost
	- Port = 9930
5. You are all set to run your own PGA!
6. For steps to register resources, applications, etc… use <Link to admin guide>
7. For steps to create projects, experiments and monitor them use <Link to end user guide>
IMPORTANT: In places where the hosted PGA link is used please replace by your locally running PGA URL.



#### <a name="PGAUbuntuOS"></a>PGA  Installation on Ubuntu OS //http://tecadmin.net/install-java-8-on-centos-rhel-and-fedora/
##### Pre-Installations
1. To install dependencies use commands in https://vpsineu.com/blog/how-to-install-laravel-on-a-centos-7-vps/
In the command avoid installing mysql and mariaDB
2. Enable the appropriate extensions: navigate to php.ini
	<pre><code>sudo vi /etc/php.ini</code></pre>
	- Uncomment the following extensions: mcrypt.so, openssl.so, and soap.so. If they do not exists add them as extensions.
	<pre><code>extension=mcrypt.so</code></pre>
	<pre><code>extension=openssl.so</code></pre>
	<pre><code>extension=soap.so</code></pre>
	- Locate httpd.conf file 
	<pre><code>sudo vi /etc/httpd/conf/httpd.conf</code></pre>
	- Find 'AllowOverride None' and change to 'AllowOverride All' (Two places to change)
	

The following guide give a sample installation starting from a fresh Ubunutu 12.04 installation. Similar instructions should be used in other operating systems.
Update the ubuntu package manager
sudo apt-get update
sudo apt-get upgrade 
Install Apache 
sudo apt-get install apache2
Install PHP 5.4
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php5-oldstable
sudo apt-get update
sudo apt-cache policy php5
sudo apt-get install php5
You can check the installed versions of apache and php using apache2 -v and php -v commands
Install the necessary php extensions
sudo apt-get install unzip
sudo apt-get install curl
sudo apt-get install openssl
sudo apt-get install php5-mcrypt
sudo apt-get install php-soap
Install Composer System Wide
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
Activate mod_rewrite
sudo a2enmod rewrite
sudo service apache2 restart
Open the default vhost config file:
 sudo nano /etc/apache2/sites-available/default. 
 Now search for “AllowOverride None”  corresponding “DocumentRoot /var/www <Directory /var/www>” (which should be there TWO times) and change both to “AllowOverride All“. Search for these two lines.
 Exit and save with CTRL+X, Y, ENTER.

Installations
 The following guide give a sample installation starting from a fresh Ubunutu 12.04 installation. Similar instructions should be used in other operating systems.
Update the ubuntu package manager
sudo apt-get update
sudo apt-get upgrade 
Install Apache 
sudo apt-get install apache2
Install PHP 5.4
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php5-oldstable
sudo apt-get update
sudo apt-cache policy php5
sudo apt-get install php5
You can check the installed versions of apache and php using apache2 -v and php -v commands
Install the necessary php extensions
sudo apt-get install unzip
sudo apt-get install curl
sudo apt-get install openssl
sudo apt-get install php5-mcrypt
sudo apt-get install php-soap
Install Composer System Wide
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
Activate mod_rewrite
sudo a2enmod rewrite
sudo service apache2 restart
Open the default vhost config file:
 sudo nano /etc/apache2/sites-available/default. 
 Now search for “AllowOverride None”  corresponding “DocumentRoot /var/www <Directory /var/www>” (which should be there TWO times) and change both to “AllowOverride All“. Search for these two lines.
 Exit and save with CTRL+X, Y, ENTER.
Download PGA from GIT
Download PGA from github to the document root of you web server /var/www. 
Use git clone https://github.com/apache/airavata-php-gateway.git or download the zip from the github web page.
Go inside the PGA directory (e.g /var/www/airavata-php-gateway)
Make sure the storage folder is writable
sudo chmod -R 755 app/storage
Go to [PGA_HOME]/app/config/pga_config.php and change the configuration to match your settings

Now issue composer install command
sudo composer install
Restart the web server
sudo service apache2 restart


#### <a name="PGACentOS"></a>PGA  Installation on Linux/CentOS //http://tecadmin.net/install-java-8-on-centos-rhel-and-fedora/
##### Pre-Installations
1. To install dependencies use commands in https://vpsineu.com/blog/how-to-install-laravel-on-a-centos-7-vps/
In the command avoid installing mysql and mariaDB
2. Enable the appropriate extensions: navigate to php.ini
	<pre><code>sudo vi /etc/php.ini</code></pre>
	- Uncomment the following extensions: mcrypt.so, openssl.so, and soap.so. If they do not exists add them as extensions.
	<pre><code>extension=mcrypt.so</code></pre>
	<pre><code>extension=openssl.so</code></pre>
	<pre><code>extension=soap.so</code></pre>
	- Locate httpd.conf file 
	<pre><code>sudo vi /etc/httpd/conf/httpd.conf</code></pre>
	- Find 'AllowOverride None' and change to 'AllowOverride All' (Two places to change)
	

##### Download and Configure PGA
1. Navigate to /var/www/html 
<pre><code>cd /var/www/html</code></pre>
2. Clone the PGA git repository:
<pre><code>sudo git clone https://github.com/apache/airavata-php-gateway.git</code></pre>
> Hint: If you get 'git not found' install git first
3. If not done earlier vi to php.ini and uncomment or add mcrypt.so, openssl.so, and soap.so
4. Create experimentData folder in html folder and give permission
make experimentData folder in html folder and I’ve permission
<pre><code> mkdir experimentData</code></pre>
chmod -R 777 app/storage
5. Copy the templat ad create a new php.config file for the gatway.
<pre><code>cp app/config/pga_config.php.template app/config/pga_config.php</code></pre>
6. Navigate to pga_config file 
<pre><code>vi app/config/pga_config.php</code></pre>
Note: make sure to make the directory pointed to by 'experiment-data-root' in pga_config.php and chmod 777 it. By default, this is /var/www/html/experimentData
7. Configure the PGA storage permissions:
<pre<code>chmod -R 777 app/storage</code></pre>
8. Update using Composer:
<pre><code>sudo composer update</code></pre>

### FAQs
1. When installing PGA in MAC i got below error after updating the composer.
	- Error
	Mcrypt PHP extension required.
	Script php artisan clear-compiled handling the post-update-cmd event returned with an error
  		[RuntimeException]
  		Error Output:
  	- Solution
  	Install mcrypt installation 
	http://coolestguidesontheplanet.com/install-mcrypt-php-mac-osx-10-10-yosemite-development-server/
	
2. After following the required steps only the home page is working and some images are not shown properly.
If you are facing this behavior first check whether you have enabled mod_rewrite module in apache webserver. And also check whether you have set AllowOverride All in the Vhost configuration file in apache web server. (e.g file location is /etc/apache2/sites-available/default and there should be two places where you want to change)
````
 <VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot /var/www/html/portal/public
    ServerName pga.example.com
    <Directory "/var/www/html/portal/public">
       AllowOverride all
    </Directory>
    ErrorLog logs/pga_error_log
    CustomLog logs/pga--access_log common
</VirtualHost>
````
3. I get the Error message Permission Denied to app/storage directory
Execute the following command and grant all permissions sudo chmod -R 777 app/storage

4. In Ubuntu environment when executing sudo composer update it fails with message Mcrypt PHP extension required.  To fix this install PHP mcrypt extension by following the below steps 
sudo apt-get install php5-mcrypt
use locate mcrypt.so ,to get its locaton
locate mcrypt.ini and open the mcrypt.ini file
sudo pico /etc/php5/mods-available/mcrypt.ini
change the at line a extension=<location of e mcrypt.so file> eg:/usr/lib/php5/20121212/mcrypt.so
save changes.
execute the command:  sudo php5enmod mcrypt
Now restart the apache server again and test PGA web-interface.

5. When tried to login or create a new user account an Error is thrown which is similar to PHP Fatal error:  SOAP-ERROR: Parsing WSDL: Couldn't load from...
If you face this kind of an error first check whether you have enabled PHP SOAP and OpenSSL extensions. If even after enabling them the issue is still occurring try updating the PHP OpenSSL extension. (Using command like yum update openssl)