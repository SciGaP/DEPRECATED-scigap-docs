# Airavata API

#### getAPIVersion
This function will give the current version been used by te user.

#### addGateway
This is to add the gateway to Airavata.

Provide:<br>
- string gatewayName	(optional)<br>
- string domain		(optional)<br>
- string emailAddress	(optional)<br>

Generates:<br>
- string gatewayId<br>

#### registerComputeResource
This is the function to use to add a compute resource in to Airavata. These resources will be used by the gateways when adding gateway preferences.

Provide:<br>
- string hostName	(required)<br>
- string resourceDescription (optional)<br>
- list<BatchQueue> batchQueues (optional)<br>
- map<fileSystems> fileSystems (optional) - Currently we don't use fileSystem information in Airavata.<br>
- list<JobSubmissionInterface> jobSubmissionInterfaces (optional)<br>
- list<DataMovementInterface> dataMovementInterfaces (optional)<br>
- i32 maxMemoryPerNode (optional)<br>	


#### createProject
Function creates a Project for the user to group experiments.

Provide:<br>
- string gatewayId	(required)<br>
- string name		(required)<br>
- string description	(required)</br>

Generates:<br>
- projectID<br>

#### updateProject
This is to update a existing project

Provide:<br>
- string projectID	(required)<br>
- string name		(required) - provide the new modified name<br>
- string description (required)- provide the new modified description<br>

#### searchProjectsByProjectName
User can search for a specific project within his projects by providing the project name or part of it.

Provide:<br>
- string gatewayId (required)<br>
- string userName	(required)<br>
- string name(required)<br>

Result:
Project list

#### searchProjectsByProjectDesc
User can search for a specific project within his projects by providing the project description or part of it.

Provide:<br>
- string gatewayId 	(required)<br>
- string userName	(required)<br>
- string description(required)<br>

Result:
Project list
