# Kura Labs Cohort 5- Deployment Workload 1
## Objectives

The purpose of this workload is to comprehensively use tools including AWS EC2, Elastic Beanstalk, GitHub, and Jenkins to simulate the CI/CD pipeline. Developers can work collaboratively on EC2 for development, use GitHub for version control, deploy through EBS, and implement CI/CD using Jenkins running on EC2.


## System diagram  
![workload_system](https://github.com/user-attachments/assets/09be32b8-fa30-4236-8088-205cc6d4f27c)


## Steps
### Working on local repository and remote repository on github
1. Init a repo on my EC2 instance
2. Pull the original repo to my initialized repo
3. Create a new repo on my Github
4. Connect the local repo to the remote repo on my github by using the personal token which is generated from GitHub.
5. Push the local repo to GitHub.
My local repository is now synced with GitHub. If further modifications are required, they can be easily shown on my GitHub repository for others to review. And this step allows developers to work collaboratively. 
### Create an EC2
The EC2 instance in this workload worked as a server. It holds the Jenkins for automatically testing and building. 
1. In the creation process, it asked about “Key Pair”, which contains the public key and private key. It is important for proving the identity and can be used to connect to this created EC2, for example to GitHub.
2. The step for configuring the security group is important for establishing a connection between the server and client or different servers. The configured security group opens port 22 for SSH, port 80 for HTTP, and port 8080 for Jenkins while filtering out other traffic.

### Run Jenkins
1. Install necessary packages to the server in order to run Jenkins on server and support the application build and test on Jenkins: sudo apt update && sudo apt install fontconfig openjdk-17-jre software-properties-common && sudo add-apt-repository ppa:deadsnakes/ppa && sudo apt install python3.7 python3.7-venv
2. Install, run and check the status of jenkins on ec2 instances.
3. Jenkins: successfully running
	<img width="606" alt="JenkinsRun" src="https://github.com/user-attachments/assets/cd313459-2a86-4a2a-8625-c21f5e492c55">


4. Login by accessing the 8080 port on the server. The address to login my jenkins is: http://ec2-54-87-219-165.compute-1.amazonaws.com:8080, which is allowed in the security group.  
	<img width="607" alt="JenkinsPass" src="https://github.com/user-attachments/assets/57b88ad7-1023-4a67-8ea4-9fb5cfa2ea20">  
	<img width="405" alt="JenkinsAdmin" src="https://github.com/user-attachments/assets/3164254c-67e9-4ed8-81e9-8be79668b511">

5. Create Multi-Branch pipeline: If the project has multiple branches, this enables automatic CI/CD for each branch. 
6. Add one branch source created in github. Once code commits to the added branch and the repository, it will trigger the test and build automatically. 
7. Build successfully
   
	<img width="609" alt="Build" src="https://github.com/user-attachments/assets/50a85d31-c817-4ed7-840e-e7b28084d08c">  

	<img width="636" alt="Build2" src="https://github.com/user-attachments/assets/0d9ee002-1127-4645-9e5c-8923f01492ef">

9.  Check the stages for this build, it has scm stage, test stage and build stage in pipeline.  
	<img width="575" alt="Stages" src="https://github.com/user-attachments/assets/b35b72ba-84bd-4b35-9872-efcec28f3a8f">

	a. Checkedout SCM: performs the function of CI, it will retrieve the latest version of code in the source version control system continuously. Manage the latest change tracked from my GitHub Retail-bank repository in this workload.
	
	b. Build Stage: Compile the code that was retrieved. If there’s any error in the source code or configuration problems, build cannot get through.
	
	c. Test stage: this is also one stage in Jenkins CI/CD that enables continuously run tests to validate the code.
	
	d.These three steps ensure that we can quickly get, build and test the program before deploying. 
	
### Elastic beanstalk
1. Create two service roles, one for Elastic Beanstalk and one for EC2. Each role has their own permissions. After these roles are created, they can be used later to gain permissions.
2. Create an “Environment” in AWS elastic beanstalk. This environment will provide the required permissions to access services by adding created two roles before, running platform.
3. Before the EBS successfully created, I met the following error. By looking at the error message, to uncheck the Activated box, the program deployed successfully.
   <img width="606" alt="Error" src="https://github.com/user-attachments/assets/ad405379-7408-4049-b607-96a9ad088ada"><img width="582" alt="TroubleShooting" src="https://github.com/user-attachments/assets/c089ab95-a55d-446e-94be-45b3cc4e6805">
5. Deployed!  
	<img width="635" alt="Deploy" src="https://github.com/user-attachments/assets/978d89ad-4de9-40eb-8b9a-dda4f028e222">  
	<img width="748" alt="image" src="https://github.com/user-attachments/assets/907d57f1-8fbf-4f51-bd79-e257ea0e37fe">


### Accessing web page
1. Click on the domain, which will translate to the IP address of the EC2 instance. Normally, we can access the resource. However, I got a 502 Bad Gateway error, indicating a server issue. With the hint, I found that the file I ‘ve uploaded is not right. And it caused the server to not run the application successfully. Before that I checked the Nginx error log and found error messages saying the connection is refused. As the following pictures.
   
	<img width="610" alt="502Error" src="https://github.com/user-attachments/assets/5604245d-cba9-4c9a-84af-2fc1d2f366fb">
	<img width="618" alt="Log" src="https://github.com/user-attachments/assets/bdc1e5f9-c27b-46dd-94a2-211ee18755cf">

3. Done!
   
	<img width="587" alt="Web" src="https://github.com/user-attachments/assets/670ee801-5d63-4008-9e77-6ff637a9ba1b">


## Optimization
## Conclusion



