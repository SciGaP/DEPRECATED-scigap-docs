# PGA Installation

[<button type="button" style="color:darkred;text-align:center;font-weight:bold;background-color:Steal;width:200px;border-radius:4px">PGA on MAC OS</button>](#headPGAMAC)  &nbsp; &nbsp; &nbsp;
[<button type="button"  style="color:darkred;text-align:center;font-weight:bold;background-color:Steal;width:200px;border-radius:4px">PGA on Cent OS</button>](#headPGACENTOS)

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

## <a name="headPGACENTOS"></a>PGA  Installation on CentOS 7
### <a name="head12345"></a>Pre-Installations
1. Install apache 
<pre><code>Yum install httpd</code></pre>
2.	module_rewrite is auto enabled in apache version in centos7. Its in /etc/httpd/conf.modules.d/00-base.conf file and the line is LoadModule rewrite_module modules/mod_rewrite.so
3.	Enable php using <pre><code>yum install php-soap</code></pre> Could be be it is already enabled in CentOS7
4. Install php using  <pre><code>yum install php</code></pre>
5. install composer
<pre><code>yum install composer</code></pre>
6. Install php-mcrypt <pre><code>yum install php-mcrypt</code></pre>

### Download and Configure PGA
1. Take the git clone https://github.com/apache/airavata-php-gateway.git
<br> Needs to take the clone in the document root. in centOS7 its var/www/html
2. Change the cloned folder name to your desired folder name(e.g.: php-gateway). This will carry sub folders for the gateway
<pre><code>cp - R airavata-php-gateway /* .</code></pre>
3. In the gateway folder do a <pre><code<composer update</code></pre>
4. Give permission to user data folder
<pre><code>chmod -R 777 /var/www/portals/gateway-user-data/php-gateway</code></pre>
5. Copy pga_config.template and make  pga_config.php
6. In pga_config.php change airavata server, change;
	-  Airavata Client Configurations
		- 'airavata-server' => 'localhost’,
		- 'gateway-id' => 'airavata_test_gateway',
		- 'experiment-data-absolute-path' => '/var/www/experimentData',(Here user has to create the experimentData folder in var/www)
		- 'gateway-data-store-resource-id' => ''
	- Portal Related Configurations
		- 'super-admin-portal' => false, (User has one gateway and need to use it to configure the compute resources, storage resources, etc...)
		- 'admin-emails' => ['airavatatest100@gmail.com'],
		- 'portal-email-username' => 'airavatatest100@gmail.com',
		- 'portal-email-password' => '&airavaxxxxxx',
	- WSO2 Identity Server Related Configurations
		- Add WSO2 IS related details URL, username, password, etc…

7. Give writing permission chmod -R g+rwx app/storage/
<br>in the http config file add URL information for the gateway file path (this is in w54 pga server) vi /etc/httpd/conf/httpd.conf
8.  Make sure SElinux comparability of airaveata_php_gateway folder. for that give chcon -Rv --type=httpd_sys_content_t airavata-php-gateway/ - this is to make sure this folder is readable by http

9. ls - lZ shows the SELinux context. after the above chcon command do the same for storage folder as well su -c "chcon -R -h -t httpd_sys_script_rw_t [fullpath]/app/storage” - this is to make sure the folder is writable

10. once the URL info added restart the http service 
<pre><code>systemctl restart  httpd.service</code></pre>

11. Configure firewall to allow http and https
<pre><code>firewall-cmd --zone=public --list-services</code></pre> - check existing configurations
<pre><code>firewall-cmd --zone=public --permanent --add-service=http</code></pre> - allow for http
<pre><code>firewall-cmd --zone=public --permanent --add-service=https</code></pre> - allow for https

<pre><code>firewall-cmd —reload - refresh</code></pre> - to get rules applied. 




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