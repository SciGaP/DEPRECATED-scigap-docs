## Follow Steps Provided in 'Gateway Configuratoin

## Troubleshooting FAQ
<br>Q1. I have setup my own gateway and Airavata. When I log into the gateway I cannot create Compute resources. What should I do?</br>
Answer: In your pga_config.php (in folder .../testdrive/app/config) under heading 'Portal Related Configurations' set 'super-admin-portal' => false, to true.</br>
<br>Q2. I don't get notifications when users create new accounts in my gateway. Why?</br>
Answer: That's because you have not defined an email address in <br>'admin-emails' => ['xxx@xxx.com','yyy@yyy.com']. Here you can add one or many.</br>
<br>Q3. I am not receiving email notifications from compute resoures for job status changes. What should I do?</br>
Answer: In airavata-server.properties please locate and set your email account information.
<pre><code>email.based.monitor.host=imap.gmail.com
email.based.monitor.address=airavata-user@kuytje.nl
email.based.monitor.password=zzzz
email.based.monitor.folder.name=INBOX
email.based.monitor.store.protocol=imaps (either imaps or pop3)</pre></code>
<br>Q4. In my Airavata log I have error messages like
<br>ERROR org.apache.airavata.api.server.handler.AiravataServerHandler  - Error occurred while retrieving SSH public keys for gateway
<br>ERROR org.apache.airavata.credential.store.server.CredentialStoreServerHandler  - Error occurred while retrieving credentials
<br>What should I do?
<br>Answer: This could be due to missing tables in your credential store database. Check whether CREDENTIALS and COMMUNITY_USER tables exits. If not create then using
<pre><code>CREATE TABLE COMMUNITY_USER
(
        GATEWAY_ID VARCHAR(256) NOT NULL,
        COMMUNITY_USER_NAME VARCHAR(256) NOT NULL,
        TOKEN_ID VARCHAR(256) NOT NULL,
        COMMUNITY_USER_EMAIL VARCHAR(256) NOT NULL,
        PRIMARY KEY (GATEWAY_ID, COMMUNITY_USER_NAME, TOKEN_ID)
);
</pre></code>
<pre><code>CREATE TABLE CREDENTIALS
(
        GATEWAY_ID VARCHAR(256) NOT NULL,
        TOKEN_ID VARCHAR(256) NOT NULL,
        CREDENTIAL BLOB NOT NULL,
        PORTAL_USER_ID VARCHAR(256) NOT NULL,
        TIME_PERSISTED TIMESTAMP DEFAULT NOW() ON UPDATE NOW(),
        PRIMARY KEY (GATEWAY_ID, TOKEN_ID)
);
</pre></code>
<br>Q5. I cannot login to my Compute Resource and launch jobs from Airavata using the SSH key I generated. What should I do?
Answer: Steps to use generated SSH key
    - Generate SSH key + token using Credential Store
    - Add the generated token to your resource through PGA --> Admin Dashboard --> Gateway Preferences
    - Add the generated SSH key