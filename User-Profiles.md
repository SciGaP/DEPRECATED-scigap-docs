# Airavata User Profiles

### What Are Airavata User Profiles?

1. When using Airavata as the middleware between your gateway and computational resources first lets identify and understand the user profiles available and their potential.
2. Knowing the profiles and the features of each will assist on shaping your gateway user hierarchy.
3. There are 4 active user profiles in Airavata with different set of features at each level.
4. 'Image - Airavata User Profiles' depicts the features available for each profile.


### What each user Profile can do within PGA?

- Super Admin
	- Super admins has access to all the gateways as well as to Airavata and PGA. Currently this role resides with limited members of SGG group at IU.
	- Create Gateway and set up identity server for user account management. 
	- Register Computer resource available to submit jobs through Airavata.
	- Add email monitoring accounts detail to Airavata for each gateway.
	- Investigate issues with individual experiments from any of the gateways under SciGaP.
<br>
<br>
- Gateway Admin	
	- Set up gateway preferences for Compute Resources and Storage Resources
	- Generate SSH keys and their tokens using Credential Store in Admin Dashboard.
	- Add the generated SSH token to Gateway Preferences.
	- Add the generated SSH keys to authorized_key files in each resource.
	- Can Cancel, clone experiments of a gateway user through Admin dashboard behalf of the user.
	- Create Applications and their deployments in to the gateway.
<br><b>NOTE: If user hosts his own gateway; 'Gateway Admin' role will hold features of both Super Admin and Gateway Admin.</b></br><br>

- Gateway Admin-Read-Only
	- Can view everything in Admin Dashboard but cannot Add, Edit or Delete any records from dashboard.
	- Can monitor experiments through Experiments Statistics in Admin dashboard.
	- Behalf of a gateway user can edit, cancel or clone an experiment.
</br>
<br>
- Gateway User
	- Create, launch their own experiments in using available applications and compute resources.
	- Monitor progress of experiment execution.
	- Group experiments by creating Projects.
	- Request new features, applications and report bug, issue using Service Desk
	- Password recovery.
</br>

