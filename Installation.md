
# Install Airavata and PGA
<b>NOTE: Below instructions are for users who host Gateway, Airavata by themselves.
<br>For communities who require SciGaP to host the gateway can contact through <a href="http://docs.scigap.org/en/latest/Contact-Us/" target="_blank">Contact Us</a></b>
<br></br>
<br><b>Select your options below;</b></br>

[<button type="button" style="color:darkblue;text-align:center;font-weight:bold;background-color:LightSteelBlue;width:200px;border-radius:4px">Airavata Installation</button>](#Airavata) &nbsp; &nbsp; &nbsp;  [<button type="button" style="color:darkblue;text-align:center;font-weight:bold;background-color:LightSteelBlue;width:200px;border-radius:4px">Airavata Configuration</button>](#AiravataConfig) <br></br>
[<button type="button" style="color:darkgreen;text-align:center;font-weight:bold;background-color:LightSteelBlue;width:200px;border-radius:4px">PGA on MAC OS</button>](#headPGAMAC)  &nbsp; &nbsp; &nbsp;  [<button type="button"  style="color:darkgreen;text-align:center;font-weight:bold;background-color:LightSteelBlue;width:200px;border-radius:4px">PGA on Cent OS</button>](#PGACentOS)
## <a name="Airavata"></a>Airavata Installation


### General Airavata Prerequisites
1. JAVA 8 or above is required
	- Java installation on CentOS, Mac, Windows, etc.. - <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html" target="_blank">Oracle JAVA Installation</a>
2. RabbitMQ
	- <a href="https://www.rabbitmq.com/download.html" target="_blank">Download the RabbitMQ Binary</a><br>Select the download file as per the operating system of your machine/server.
	- Same link has installing guide documentation as well. E.g.:<a href="https://www.rabbitmq.com/install-standalone-mac.html" target="_blank">MAC Installation Guide</a>
	- For  detailed information on getting RabbitMQ started, stoped, etc please visit <a href="https://www.rabbitmq.com/documentation.html" target="_blank">RabbitMQ Documentation</a>
3. Maven
	- <a href="http://maven.apache.org/download.cgi" target="_blank">Download Maven</a> (java based code building tool).
4. MySQL Database

### Airavata Installation on CentOS 7
<b>NOTE: Airavata installation on other operating systems are similar with minor changes.</b></br>
#### Prerequisites
1. CentOS 7 Default open JDK 1.8.0. (minimum) is sufficient.
2. Download RabbitMQ binary for CentOS 7
<a href="https://https://www.rabbitmq.com/install-generic-unix.html" target="_blank">Download RabbitMQ Binary for CentOS</a><br>
3. Prerequisite for RabbitmQ Erlang can be installed using yum
<pre><code>yum install Erlang</code></pre>
4. Unzip the downloaded RabbitMQ tar file into a folder in your local machine.
<pre><code>tar -xvf rabbitmq-server-mac-standalone-3.4.1.tar.gz</code></pre>
5. Start the RabbitMQ server in the bin folder using;
 <pre><code>./sbin/rabbitmq-server start</code></pre>
6. Install Maven using yum install. ((install the latest maven 3.3.9. Default Maven default of centOS 7).
<pre><code>yum install maven</code></pre>
7. Install MySQL database
<pre><code>yum install mariadb-server</code></pre>
8. Start maria DB with;
<pre><code>systemstl start mariadb</code><pre>
9. While maria DB is running run
<pre><code>mysql _secure_installation</code></pre>
When executing above it will ask you for root password; provide it.
10. Create databases required for Airavata
<pre><code>create database airavata_appcatalog;</code></pre>
<pre><code>create database airavata_expcatalog;</code></pre>
<pre><code>create database airavata_datacatalog;</code></pre>
<pre><code>create database airavata_credentialstore;</code></pre>
<pre><code>create database airavata_wfcatalog;</code></pre>
11. Grant permission to these databases for Airavata<br>
Command syntax: <pre><code>grant all privileges on 'DB-Name'.<p>&#x204E; to 'username'@'%' identified by 'password’;</code></pre>
E.g.: <pre><code>grant all privileges on airavata_appcatalog.<p>&#x204E; to 'airavatadb'@'%' identified by 'airavatadb’;</code></pre>
NOTE: Grant permission to every databased created above. % can be replaced by  'localhost' (if DB is also in the same server as airavata). If DB is in a different server give the server name.
<br>

#### Install Airavata
1. Create a folder in your local machine (E.g.: mkdir LocalAiravata).<br>
2. Clone the master source (If you have not taken a clone prior) code from github to the created folder.<br>
<pre><code>git clone https://github.com/apache/airavata.git</code></pre>
3. After cloning is completed, build the source code by executing following maven command (In LocalAiravata directory you made);
<pre><code>mvn clean install</code></pre>
Hint: To avoid tests (recommended for first time users) use
<pre><code>mvn clean install -Dmaven.test.skip=true</code></pre>
4. Locate the tar file in target directory
Path:
<pre><code>cd airavata/distribution/target/</code></pre>
5. Navigate to locally created directory (LocalAiravata) copy the tar file
<pre><code>cp airavata/distribution/target/apache-airavata-server-0.16-SNAPSHOT-bin.tar.gz ./</code></pre>
OR
<pre><code>cp airavata/distribution/target/apache-airavata-server-0.16-SNAPSHOT-bin.tar.zip ./</code></pre>
6. Now unzip either the tar or zip file of Airavata server distribution;
<pre><code>unzip apache-airavata-server-0.16-SNAPSHOT-bin.zip</code></pre>
OR
<pre><code>tar xvzf apache-airavata-server-0.16-SNAPSHOT-bin.tar.gz</code></pre>
7. Generate Credential store keystore file in the created local directory.
<pre><code>	keytool -genseckey -alias airavata -keyalg AES -keysize 128 -storetype jceks -keystore airavata_sym.jks</code></pre>
For more information visit <a href="https://cwiki.apache.org/confluence/display/AIRAVATA/Credential+Store+Configuration+Guide/" target="_blank">Credential Store Configuration Documentation</a>
8. Navigate to bin folder which contains file airavata-server.properties and open it;
<pre><code>vi apache-airavata-server-0.16-SNAPSHOT/bin</code></pre>
9. Update relevant necessary properties to run Airavata locally.<br>
Change as required;
	- API Server Registry Configuration
		- Comment out the derby DB properties
		- Change MySQL configurations
			- registry.jdbc.url=jdbc:mysql://localhost:3306/airavata_expcatalog (replace 'localhost' with correct server name if the DB is in a different server)
			- registry.jdbc.user=airavata
			- registry.jdbc.password=airavata
			- default.registry.gateway=php_reference_gateway (give the gateway name you prefer. Default exists in the file)
   	- Application Catalog DB Configuration
   		- Comment out the derby DB properties
   		- Change MySQL configurations
   			- appcatalog.jdbc.url=jdbc:mysql://localhost:3306/airavata_appcatalog
          	- appcatalog.jdbc.user=airavata
         	- appcatalog.jdbc.password=airavata
    - Data Catalog DB Configuration
    	- Comment out the derby DB properties
        - Change MySQL configurations
    		- datacatalog.jdbc.url=jdbc:mysql://localhost:3306/airavata_datacatalog
        	- datacatalog.jdbc.user=airavata
        	- datacatalog.jdbc.password=airavata
	- Workflow Catalog DB Configuration
		- Comment out the derby DB properties
        - Change MySQL configurations
			- workflowcatalog.jdbc.url=jdbc:mysql://localhost:3306/airavata_wfcatalog
      		- workflowcatalog.jdbc.user=airavatadb
      		- workflowcatalog.jdbc.password=airavatadb
	- Server module Configuration
		- Make sure all servers required to start are added as given
			- servers=apiserver,orchestrator,gfac,credentialstore
	- API Server SSL Configurations
		- Give the correct path for key generation file. This is in the bin directtory and it is shipped defualt with Airavata.
			- apiserver.keystore=/home/airavata/LocalAiravata/apache-airavata-server-0.16-SNAPSHOT/bin/airavata.jks
	- Credential Store module Configuration
		- Make sure its'true' in
			- start.credential.store=true
		- Add the path to SSH key generation file
			- E.g.: credential.store.keystore.url=/home/airavata/LocalAiravata/airavata-sym.jks
		- Comment out the derby DB properties
        - Change MySQL configurations
        	- credential.store.jdbc.url=jdbc:mysql://localhost:3306/airavata_credentialstore
            - credential.store.jdbc.user=airavatadb
            - credential.store.jdbc.password=airavatadb
		- credential.store.keystore.url=/home/airavata/production-deployment/airavata_sym.jks
	-  API Security Configuration
		- Make sure
			- api.secured=false
			- TLS.enabled=false
	- AMQP Notification Configuration
		- 


10. In bin start the Airavata server; This may require JAVA_HOME to be defined. Some configurations such as in  bin/zoo.cfg and bin/airavata-server.properties  may have to be adjusted if some ports are already in use. Ports need to be open as well.
<pre><code>sh airavata-server.sh start</code></pre> (This will run the airavata server in the background in demon mode)<br>
11. If you are in the target folder use given to start Airavata server;<br>
<pre><code>sh apache-airavata-server-0.16-SNAPSHOT/bin/airavata-server.sh start</code></pre>
12. To monitor the server starting up, view the airavata server log;<br>
<pre><code>tail -f airavata-server.out</code></pre>	
13. For subsequent Airavata copies; in the local Airavata folder where source code is cloned do a git clone https://github.com/apache/airavata.git for the latest trunk.


### <a name="AiravataConfig"></a>Configurations
1. If you are using your own MySQL database go and put mysql.jar in to lib of Airavata. navigate to lib;
<pre><code>cd /LocalFolderPath/apache-airavata-server-0.16-SNAPSHOT/lib</code></pre>
2. Navigate to airavata-server.properties file in bin folder and change;
	- Comment out derby DB configuration parts.
	- Add MySQL Database configurations
<pre><code>#MySql database configuration
          registry.jdbc.driver=com.mysql.jdbc.Driver
          registry.jdbc.url=jdbc:mysql://xxxx.iu.xsede.org:3333/dev_expcatalog_3333
          registry.jdbc.user=SampleUser
          registry.jdbc.password=SampleUserPassword</code></pre>
	-  Under 'Monitoring Module Configuration' monitoring email account details
<pre><code>#These properties will used to enable email base monitoring
           email.based.monitor.host=imap.gmail.com
           email.based.monitor.address=jobs@sample.org
           email.based.monitor.password=SamplePassword
           email.based.monitor.folder.name=INBOX
           # either imaps or pop3
           email.based.monitor.store.protocol=imaps</code></pre>

<br></br>
# PGA Installation

## <a name="head1234"></a>General PGA Prerequisites
1. A Unix or Unix like operating system
2. A web server (e.g apache web server) with PHP 5.4 or higher. Make sure have enabled mod_rewrite module in httpd.conf file and enable PHP SOAP extension
3. Composer
4. MYSQL database (Required if the user is hosting Airavata on his own. To communicate with hosted Airavata this step is not relevant)
5. MCrypt PHP extension
6. Enable OpenSSL PHP extension
7. Follow instructions given in links to install the prerequisites based on the OS ;
	- On Ubunutu: http://www.dev-metal.com/install-laravel-4-ubuntu-12-04-lts/
	- On Centos: https://www.digitalocean.com/community/tutorials/how-to-install-laravel-4-on-a-centos-6-vps
	- On MAC OS: http://sangatpedas.com/20140219/installing-laravel-osx-mavericks/
8. Important: Do not need to install Laravel. You can skip the steps given on the links
9. WSO2 IS server


## <a name="headPGAMAC"></a>PGA  Installation on MAC Yosemite OS
### <a name="head12345"></a>Pre-Installations
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

### Download and Configure PGA
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
6. You might get an error like this
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

###Link Airavata and PGA
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


## <a name="PGAUbuntuOS"></a>PGA  Installation on Ubuntu OS
//http://tecadmin.net/install-java-8-on-centos-rhel-and-fedora/
### Pre-Installations
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


### Download and Configure PGA
1. The following guide give a sample installation starting from a fresh Ubunutu 12.04 installation. Similar instructions should be used in other operating systems.
2. Update the ubuntu package manager
<pre><code>sudo apt-get update</pre></code>
<pre><code>sudo apt-get upgrade </pre></code>
3. Install Apache
</pre></code>sudo apt-get install apache2</pre></code>
4. Install PHP 5.4
<pre><code>sudo apt-get install python-software-properties</pre></code>
<pre><code>sudo add-apt-repository ppa:ondrej/php5-oldstable</pre></code>
<pre><code>sudo apt-get update</pre></code>
<pre><code>sudo apt-cache policy php5</pre></code>
<pre><code>sudo apt-get install php5</pre></code>
4. You can check the installed versions of apache and php using <pre><code>apache2 -v</pre></code> and <pre><code>php -v commands</pre></code>
5. Install the necessary php extensions
<pre><code>sudo apt-get install unzip</pre></code>
<pre><code>sudo apt-get install curl</pre></code>
<pre><code>sudo apt-get install openssl</pre></code>
<pre><code>sudo apt-get install php5-mcrypt</pre></code>
<pre><code>sudo apt-get install php-soap</pre></code>
6. Install Composer System Wide
<pre><code>curl -sS https://getcomposer.org/installer | php</pre></code>
<pre><code>sudo mv composer.phar /usr/local/bin/composer</pre></code>
7. Activate mod_rewrite
<pre><code>sudo a2enmod rewrite</pre></code>
<pre><code>sudo service apache2 restart</pre></code>
8. Open the default vhost config file:
 <pre><code>sudo nano /etc/apache2/sites-available/default. </pre></code>
9. Now search for “AllowOverride None”  corresponding “DocumentRoot /var/www <Directory /var/www>”
<br>(which should be there TWO times) and change both to “AllowOverride All“. Search for these two lines.</br>
10. Exit and save with CTRL+X, Y, ENTER.

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


## <a name="PGACentOS"></a>PGA  Installation on Linux/CentOS //http://tecadmin.net/install-java-8-on-centos-rhel-and-fedora/
### Pre-Installations
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
	

### Download and Configure PGA
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
5. Copy the template ad create a new php.config file for the gatway.
<pre><code>cp app/config/pga_config.php.template app/config/pga_config.php</code></pre>
6. Navigate to pga_config file 
<pre><code>vi app/config/pga_config.php</code></pre>
Note: make sure to make the directory pointed to by 'experiment-data-root' in pga_config.php and chmod 777 it. By default, this is /var/www/html/experimentData
7. Configure the PGA storage permissions:
<pre<code>chmod -R 777 app/storage</code></pre>
8. Update using Composer:
<pre><code>sudo composer update</code></pre>

## FAQs
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