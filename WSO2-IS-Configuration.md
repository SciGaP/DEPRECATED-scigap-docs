## WSO2 IS (Identity Server)

The steps are for IS configuration when IS is hosted by AIravata team. n this situation you will be a tenant created under Airavata hosted IS.

### First You Need to;
1. Request from Airavata team for a new Tenant account. For this use
<br><a href="http://airavata.apache.org/community/mailing-lists.html" target="_blank">Airavata mailing list</a>
OR
<a href="https://www.hipchat.com/gMDHyN1KM" target="_blank">HipChat</a>
2. As the gateway admin, for the account creation provide;
    - First name
    - Last name
    - Preferred username & password as the admin (This is the username you will use to login to WSO2 IS and gateway as the admin user)
    - Email account
3. Once the tenant is created you will receive
    - URL for WSO2 IS
    - Username and password to login to WSO2 IS
<br>
<br>
### Configuration
1. Login to IS server as the gateway admin; Tenant user.
    - Use the URL provided by the Airavata team; <a href="https://idp.scigap.org:9443/carbon/admin/login.jsp" target="_blank">WSO2 URL for Gateway Admin</a>
    - Use the username and password provided by you. (Please change your password in first login)
2. Navigate to Main Tab -->Service Providers --> Add
    - Give a service provider name and 'Register'
    - Out of the list below expand 'Inbound Authentication Configuration'
    - Out of the usb list underneath expand 'OAuth/OpenID Connect Configuration' and click 'Configure'
    - You will be navigated to 'Register New Application' UI.
3. To register new application;
    - Select OAuth Version = 2.0
    - From Allowed Grant Types select only 'Password' and 'Refresh Toekn'
    - Add
    
4. Copy the 'OAuth Client Key', 'OAuth Client Secret', Admin username, password and name to pga_config.php.
5. Navigate to Configure —> Claim management —>http://wso2.org/claims. And make "Supported by Default = true"
6. Navigate to Configure --> Users & Roles --> Users. Find the admin user and click 'User Profile'. Add the username at the bottom and update.

You are all set to start configuring the gateway for job submission. For Gateway Configurations visit <a href="#Gateway-Configuration.md">PGA Configuration</a>
