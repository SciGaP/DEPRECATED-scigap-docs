## PGA Configurations
### You Need to Have
1. Airavata & PGA installed and running
2. Tenant created in WSO2 IS hosted by you or SGG
3. Administrator privileges to the gateway with username and password
<br>
<br>
### Airavata Component Configuration
1. For this we use 'Admin Dashboard'
2. Gateway Admin need to configure;<br>
	- <a href="#CompResource">Compute Resources</a><br>
	- <a href="#CompResource">Compute Resources</a><br>
	- <a href="#StoreResource">Storage Resources</a><br>
	- <a href= "#Preference">Resource Preferences</a><br>
	- <a href= "#AppCatalog">Application Catalog</a><br>
		- Application Module<br>
		- Application Interface<br>
		- Application Deployment<br>
	- <a href= "#Credentials">Credential Store</a>
		- Generate Credential Store Token + SSH Key.
		- Add these to authorized key files and into preferences.
<br>
<br>
###<h3 id="CompResource">Compute Resources</h3>
1. Navigate to Admin Dashboard --> Compute Resources --> Register
2. Add Host Name, Description and create the resource.
3. Then add data storage information in
	- Data Movement Interfaces
4. And Save.
5. Similarly you can add multiple storage resources in to your gateway by selecting 'Register' from the left-hand-side menu.
6. To view the added resources navigate to Admin Dashboard --> Storage Resources --> Browse
7. All the resources will be listed. Gateway admin can view, edit, delete them.
NOTE: Currently enabling and disabling storage resources is not an active feature.
<br>
<br>
###<h3 id="StoreResource">Storage Resources</h3>
1. Navigate to Admin Dashboard --> Storage Resources --> Register
2. Add Storage Name, Description and create the resource.
3. Then keep adding information on rest of the tabs appeared.
	- Queues
	- File Systems (Not required at the moment)
	- Job Submission Interfaces
	- Data Movement Interfaces
4. And Save.
5. Similarly you can add multiple compute resources in to your gateway by selecting 'Register' from the left-hand-side menu.
6. To view the added compute resources navigate to Admin Dashboard --> Compute Resource --> Browse
7. All the resources will be listed. Gateway admin can view, edit, delete and enable and disable them.
<br>
<br>
###<h3 id="Preference">GatewayPreferences for Resources</h3>
1. Navigate Admin Dashboard --> Gateway Preferences
2. Both compute resource and storage resource specific preferences are defined here.
3. To add compute resource related preferences click "Add a Compute Resource Preferences" and select the resource from the drop-down list.
4. Add/select preferred options and click "Set preferences". Repeat this for all the resources used within the gateway.
<br>Repeat this for every active enabled compute resource in the gateway.
4. For each compute resource, gateway admin need to;
  	- whether the preferences can be overridden by Airavata - Yes/No
  	- Resource login name
  	- Preferred job submission and data movement protocols
  	- Preferred queue
  	- Scratch location
  	- Project allocation number
  	- Resource specific credential store token
5. For adding storage resource preference click "Add a Storage Resource Preferences", and rest is similar to adding a compute resource preference.
6. For a gateway currently when a storage resource is selected, that resource ID need to be added in to the pga_config.php file in config folder of the hosted gateway.
7. For storage resource preference, gateway admin need to add;
	- Login username
	- File System Root Location
	- Resource Specific Credential Store Token
8. Apart from adding preference the same interface is used to assign a 'Base Credential Store Token". If this is added this is the token used across the gateway for communication with all the compute resources and storage resource.
<br>
<br>
### <h3 id="AppCatalog">Application Catalog</h3>
1. Gateway admin add applications in to the gateway. Adding an application is a 3 step process.
2. Admin need to add application module, interface and deployment information in order to launch specific application jobs on compute resources.
3. What each step means?
	- <b class="blue">Application Module</b>
		- Navigation: Admin Dashboard --> App Catalog --> Module
		- This is the simple introduction of the application; Name, Version and Description.
		- Click on 'Create a New Application Module' and provide information.
		- Click Create.
		- All available modules are also listed; admin has the option of searching for a particular module by providing the name in the search.
		- Gateway admin can edit, delete existing modules.
		- Deleting a module will be restricted if it has application interfaces and deployments linked.
	- <b class="blue">Application interface</b>
		- Navigation: Admin Dashboard --> App Catalog --> Interface
		- Application interface defines the required inputs, output produced and their characteristics.
		- Click on 'Create a New Application Interface' and provide information.
        - Click Create.
        - All available interfaces are also listed; admin has the option of searching for a particular interface by providing the name in the search.
        - Gateway admin can edit, delete existing interfaces.
        - Gateway admin cal also clone an existing interface in order to create a new similar interface with slight changes.
	- <b class="blue">Application deployment</b>
		- Navigation: Admin Dashboard --> App Catalog --> Deployment
			- Application deployment describes application deployment details on a specific resource.
			- For an application for each resource there is a separate deployment.
<br>
<br>
### <h3 id="Credentials">Credential Store</h3>
1. Navigation: Admin Dashboard --> Credential Store
2. This interface is used to generate SSH key + token pairs.
3. These generated keys can be added in to the authorized key files in each resource for SSH key based communication.
4. When generated key can be either assigned at gateway level; one key + token pair  for all the resources OR have separate keys for each resource.
5. SSH keys are used for communication with compute resources and storage resources.

### <h3 id="Preference">WSO2 IS Configuration</h3>
1. Setting up WSO2 IS for the new gateway.
2. Once PGA is cloned all information related to user identity will be in app/config/pga_config.php. No modifications required for users who are using 	hosted IS.
3. For user identity management we could either use Airavata WSO2 IS or users own WSO2 IS.
4. Download WSO2 Identity Server 5.0 from http://product-dist.wso2.com/products/identity-server/5.0.0/wso2is-5.0.0.zip
5. Extract the downloaded IS binary archive to a location <IS_HOME>.
6. Set JAVA_HOME variable and add jdk bin directory to the PATH variable.
7. Open <IS_HOME>/repository/conf/carbon.xml and change the following property to false
<HideAdminServiceWSDLs>false</HideAdminServiceWSDLs>
8. Execute the following command to run the server
sh <IS_HOME>/bin/wso2server.sh
You should be able to login to the Identity Server Web App using your browser with url http://localhost:9443/carbon . Default admin credentials are username: admin, password: admin
9. For more information regarding WSO2 Identity Server refer this https://docs.wso2.org/display/IS460/Deploying+in+Production
Gateway admin will be provided with
	- Domain URL for the Gateway
	- Admin User name



	

