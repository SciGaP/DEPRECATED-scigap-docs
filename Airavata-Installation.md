
## Install Airavata
<b>NOTE: Below instructions are for users who host Airavata by themselves.
<br>For communities who require SciGaP to host the gateway can contact through <a href="http://docs.scigap.org/en/latest/Contact-Us/" target="_blank">SciGaP - Contact Us</a></b>
<br></br>
<br><b>Click your option;</b></br>

[<button type="button" style="color:darkred;text-align:center;font-weight:bold;background-color:Steal;width:200px;border-radius:4px">Airavata Prerequisites</button>](#Airavata) &nbsp; &nbsp; &nbsp;
[<button type="button" style="color:darkred;text-align:center;font-weight:bold;background-color:Steal;width:200px;border-radius:4px">Airavata on CentOS 7</button>](#AiravataCent) <br></br>


### <h3 id="Airavata">General Airavata Prerequisites</h3>
1. JAVA 8 or above is required
	- Java installation on CentOS, Mac, Windows, etc.. - <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html" target="_blank">Oracle JAVA Installation</a>
2. RabbitMQ
	- <a href="https://www.rabbitmq.com/download.html" target="_blank">Download the RabbitMQ Binary</a><br>Select the download file as per the operating system of your machine/server.
	- Same link has installing guide documentation as well. E.g.:<a href="https://www.rabbitmq.com/install-standalone-mac.html" target="_blank">MAC Installation Guide</a>
	- For  detailed information on getting RabbitMQ started, stopped, etc please visit <a href="https://www.rabbitmq.com/documentation.html" target="_blank">RabbitMQ Documentation</a>
3. Maven
	- <a href="http://maven.apache.org/download.cgi" target="_blank">Download Maven</a> (java based code building tool).
4. MySQL Database

### <a name="#AiravataCent"></a>Airavata Installation on CentOS 7
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
8. Go and put mysql.jar in to lib of Airavata. navigate to lib;
   <pre><code>cd /LocalFolderPath/apache-airavata-server-0.16-SNAPSHOT/lib</code></pre>
9. Navigate to bin folder which contains file airavata-server.properties and open it;
<pre><code>vi apache-airavata-server-0.16-SNAPSHOT/bin</code></pre>
10. Update relevant necessary properties to run Airavata locally.<br>
Change as required;<a href="../Installations/airavata-properties.md">test</a>
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
	-  Monitoring Module Configuration
      	- Add your email address, username and password for email monitoring. This is the email account the job status change emails will be received from compute resources.
                 email.based.monitor.host=imap.gmail.com
                 email.based.monitor.address=jobs@sample.org
                 email.based.monitor.password=SamplePassword
	-  Zookeeper Server Configuration
		- For 'Production' scenario make;
			- embedded.zk=false
	- AMQP Notification Configuration
		- Users can use RabbitMQ as 'Guest' users. This is the easy method. For this uncomment
			- rabbitmq.broker.url=amqp://localhost:5672
		- To use as a 'Production' user
			- Navigate to RabbitMQ bin folder.
			- Make sure the RabbitMQ server is running. For production use <pre><code>rabbitmq-server -detached</code></pre> to start.
			- Create a virtual-host and user with a password. Follow documentation in <a href="http://blog.dtzq.com/2012/06/rabbitmq-users-and-virtual-hosts.html" target="_blank">RabbitMQ Users & VirtualHost</a>
			- To create a user; <pre><code>rabbitmqctl add_user Username Password</code></pre>
			- To create a vitrual-host <pre><code>rabbitmqctl add_vhost vhostauthvhost</code></pre>
			- Provide permission to created 'Username'  to the created vhost <pre><code>rabbitmqctl set_permissions -p messaging airavata ".*" ".*" ".*”</code></pre>
			- Uncomment rabbitmq.broker.url=amqp://Username:Password@localhost:5672/Vhost. Add the created username, password and Vhost in the URL.
			- If you need to stop RabbitMQ use <pre><code>rabbitmqctl stop</code></pre>.
			  <br> If the RabbitMQ server stopped then the above user creation, vhost cretion and permission granting commmands need to run again after restarting the servers.
11. Download and install Zookeeper. Use <a href=" http://www.us.apache.org/dist/zookeeper/zookeeper-3.4.8/" target="_blank">Download Zookeeper</a> <br> You can downlaod and install Zookeeper in the above created local folder; LocalAiravata
12. Navigate to the Zookeeper bin directory  and start zookeeper <pre><code>zkServer.sh start</code></pre>
13. In bin start the Airavata server and monitor log messages; This may require JAVA_HOME to be defined. Some configurations such as in  bin/zoo.cfg and bin/airavata-server.properties  may have to be adjusted if some ports are already in use. Ports need to be open as well.
<pre><code>sh airavata-server.sh start</code></pre> (This will run the airavata server in the background in demon mode)<br>
14. If you are in the target folder use given to start Airavata server;<br>
<pre><code>sh apache-airavata-server-0.16-SNAPSHOT/bin/airavata-server.sh start</code></pre>
15. To monitor the server starting up, view the airavata server log;<br>
<pre><code>tail -f airavata-server.out</code></pre>	
16. For subsequent Airavata copies; in the local Airavata folder where source code is cloned do a git clone https://github.com/apache/airavata.git for the latest trunk.