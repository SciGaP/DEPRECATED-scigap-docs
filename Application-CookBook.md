## Application Cookbook Recipes 

### Airavata Applications and Available Resource List
|  	Application  	|  		Resource List  		|
|:-----------------	|:--------------------------|
| Abinit           	| BigRed2					|
| Amber_Sander     	| BigRed2, Stampede, Comet	|
| AutoDock         	| BigRed2					|
| CP2K             	| BigRed2					|
| Echo             	| BigRed2, Stampede, Comet	| 
| Gamess           	| BigRed2, Gordon			|
| Gaussian         	| BigRed2, Comet, Gordon	|
| Gromacs          	| BigRed2, Stampede			|
| Lammps           	| BigRed2, Stampede, Comet	|
| NEK5000          	| BigRed2					|
| NWChem           	| Stampede, Comet			|
| Phasta_P         	| Stampede					|
| Quantum_Espresso 	| Stampede, Comet			|
| Tinker_Monte     	| Stampede					|
| WRF				| Stampede					|



### Application Inputs
Inputs for all applications currently available in Airavata can be found in
https://iu.box.com/s/9ztdby709kso8siachz16svn2y511nn7 



### Sample Application Recipes
#### Abinit
###### Module
- Name: Abinit
- Description: A package whose main program allows one to find the total energy, charge density and electronic structure of systems made of electrons and nuclei (molecules and periodic solids) within Density Functional Theory (DFT)	
###### Interface 
- Inputs: 		
	- Pspgth-Input-File
	- Tbase-Input-File-1
	- Tbase-Input-File-2
- Outputs:
	- Application-Out
	- Standard-Error
	- Standard-Out
###### Deployment

| 		Resource 	| 				Executable Path 			| Application Parallelism	| 								Module Load Commands								|
|:------------------|:------------------------------------------|:--------------------------|:----------------------------------------------------------------------------------|
|bigred2.uits.iu.edu| /N/soft/cle4/abinit/cpu/7.6.4/bin/abinit	| CRAY_MPI					| module swap PrgEnv-cray/5.2.40 PrgEnv-gnu/5.2.40; module load netcdf fftw abinit	|


#### Amber_sander
- Name: Amber_Sander
- Description: 	Assisted Model Building with Energy Refinement MD Package
- Inputs:
	- Heat-Restart-File
	- Parameter-Topology-File 
	- Production-Control-File
- Outputs:
	- Amber-Execution-log
	- Amber-Execution-Summary 
	- Amber-Restart-File
	- Amber-Trajectory-File
	- Standard-Error
	- Standard-Out
- Deployment

| 		Resource 		 | 				Executable Path 								| Application Parallelism	| 								Module Load Commands			   |
|:------------------	 |:----------------------------------------------------------	|:--------------------------|:-----------------------------------------------------------------|
| bigred2.uits.iu.edu	 | /N/soft/cle4/amber/gnu/mpi/12/amber12/bin/sander.MPI -O		| MPI						| module load amber/gnu/mpi/12; module swap PrgEnv-cray PrgEnv-gnu |
| stampede.tacc.xsede.org| /opt/apps/intel13/mvapich2_1_9/amber/12.0/bin/sander.MPI -O	| MPI						| module load amber												   |
| comet.sdsc.edu		 | /opt/amber/bin/sander.MPI									| MPI						| module load amber												   |


#### AutoDock
- Name: AutoDock
- Description: 	AutoDock suite of automated docking tools
- Inputs:
	- HSG1-Maps-FLD
	- Input-File-DAT 
	- Input-File-DPF
- Outputs:
	- Standard-Error
	- Standard-Out
- Deployment

| 		Resource 		 | 				Executable Path 				| Application Parallelism	| 	Module Load Commands	  |
|:------------------	 |:---------------------------------------------|:--------------------------|:----------------------------|
| bigred2.uits.iu.edu	 | /N/soft/cle4/autodock/4.2/bin/autodock4		| MPI						| module load autodock/4.2 	  |


##### CP2K
- Name: CP2K
- Description: 	CP2K Test Application Module
- Inputs:
	- Input-File-INP
- Outputs:
	- CP2K-Application-Output
	- Standard-Error
	- Standard-Out
- Deployment

| 		Resource 	 | 		Executable Path 		| Application Parallelism	| 	Module Load Commands  |
|:-----------------	 |:-----------------------------|:--------------------------|:------------------------|
| comet.sdsc.edu	 | /opt/cp2k/bin/cp2k.popt		| MPI						| module load cp2k		  |


##### Echo	
- Name: CP2K
- Description: 	A Simple Echo Application
- Inputs:
	- Input-to-Echo
- Outputs:
	- Standard-Error
	- Standard-Out
- Deployment

| 		Resource 		 | 				Executable Path 								| Application Parallelism	| 		Module Load Commands	 |
|:------------------	 |:----------------------------------------------------------	|:--------------------------|:-------------------------------|
| bigred2.uits.iu.edu	 | /N/u/seagrid/BigRed2/production/app_wrappers/echo_wrapper.sh	| SERIAL					|  								 |
| stampede.tacc.xsede.org| /home1/02731/scigap/apps/echo_wrapper.sh						| SERIAL					| 								 |
| comet.sdsc.edu		 | /home/scigap/apps/echo_wrapper.sh							| SERIAL					| 								 |
