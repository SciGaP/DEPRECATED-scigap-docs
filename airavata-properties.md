##<h2 id="airavata-properties.md">Airavata Server Properties</h2>
1.  API Server Registry Configuration
	- Comment out the derby DB properties
	- Change MySQL configurations
		- registry.jdbc.url=jdbc:mysql://localhost:3306/airavata_expcatalog (replace 'localhost' with correct server name if the DB is in a different server)
		- registry.jdbc.user=airavata
		- registry.jdbc.password=airavata
		- default.registry.gateway=php_reference_gateway (give the gateway name you prefer. Default exists in the file)
2.  Application Catalog DB Configuration
   	- Comment out the derby DB properties
   	- Change MySQL configurations
   		- appcatalog.jdbc.url=jdbc:mysql://localhost:3306/airavata_appcatalog
          - appcatalog.jdbc.user=airavata
         - appcatalog.jdbc.password=airavata
3.  Data Catalog DB Configuration
    - Comment out the derby DB properties
    - Change MySQL configurations
    	- datacatalog.jdbc.url=jdbc:mysql://localhost:3306/airavata_datacatalog
        - datacatalog.jdbc.user=airavata
        - datacatalog.jdbc.password=airavata
4.  Workflow Catalog DB Configuration
	- Comment out the derby DB properties
    - Change MySQL configurations
		- workflowcatalog.jdbc.url=jdbc:mysql://localhost:3306/airavata_wfcatalog
      	- workflowcatalog.jdbc.user=airavatadb
      	- workflowcatalog.jdbc.password=airavatadb
5.  Server module Configuration
	- Make sure all servers required to start are added as given
		- servers=apiserver,orchestrator,gfac,credentialstore
6.  API Server SSL Configurations
	- Give the correct path for key generation file. This is in the bin directtory and it is shipped defualt with Airavata.
		- apiserver.keystore=/home/airavata/LocalAiravata/apache-airavata-server-0.16-SNAPSHOT/bin/airavata.jks
7.  Credential Store module Configuration
	- Make sure its 'true' in
		- start.credential.store=true
	- Add the path to SSH key generation file
		- E.g.: credential.store.keystore.url=/home/airavata/LocalAiravata/airavata-sym.jks
	- Comment out the derby DB properties
    - Change MySQL configurations
        - credential.store.jdbc.url=jdbc:mysql://localhost:3306/airavata_credentialstore
        - credential.store.jdbc.user=airavatadb
        - credential.store.jdbc.password=airavatadb
		- credential.store.keystore.url=/home/airavata/production-deployment/airavata_sym.jks
8.   API Security Configuration
	- Make sure
		- api.secured=false
		- TLS.enabled=false
9.  Monitoring Module Configuration
      - Add your email address, username and password for email monitoring. This is the email account the job status change emails will be received from compute resources.
                 email.based.monitor.host=imap.gmail.com
                 email.based.monitor.address=jobs@sample.org
                 email.based.monitor.password=SamplePassword
10. Zookeeper Server Configuration
	- For 'Production' scenario make;
		- embedded.zk=false
11. AMQP Notification Configuration
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
		- If you need to stop RabbitMQ use <pre><code>rabbitmqctl stop</code></pre>
		If the RabbitMQ server stopped then the above user creation, vhost cretion and permission granting commmands need to run again after restarting the servers.
