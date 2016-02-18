# Airavata Is....

- A distributed framework that supports execution and management of computational scientific applications and workflows in grid based systems, remote clusters and cloud based systems.
- Airavata’s main focus is on submitting and managing application executions and workflows in grid based systems.
- Airavata’s architecture is extensible to support for other underlying resources as well.
- Traditional scientific applications provide a portal for users to submit and manage scientific applications which is called as science gateways.
- Airavata can be used by scientific gateway developers as their middleware layer. They can directly call Airavata API in order to communicate with grid based system.

# How do you want to use Airavata?

Two options; </br>
1. Gateway hosted by SciGaP<br>
    - Provided you have your own allocatoin you can use all compute resource available within Airavata.<br>
    - SciGaP will host WSO2 IS, MySQL DB for you and als the gateway in SciGaP servers.<br>
<br>
<br>2. Gateway hosted by User<br>
    - You have to install all pre requisites such as RabbitMQ, My SQL, etc<br>
    - User installs and hosts Airavata, PGA and WSO2 IS on own servers.<br>
    - Configure and register all compute resources, Gateway configuration on your own<br>


Based on the option you select the level of assistance you receive from Airavata group will differ. 
SciGaP or Airavata team will always act as the consultants to science communities and users who are looking out for middleware and gateways.
