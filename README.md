# Kura Labs Cohort 5- Deployment Workload 1
## Objectives

The purpose of this workload is to comprehensively use tools including AWS EC2, Elastic Beanstalk, GitHub, and Jenkins to simulate the CI/CD pipeline. Developers can work collaboratively on EC2 for development, use GitHub for version control, deploy through EBS, and implement CI/CD using Jenkins running on EC2.


## System diagram
 System diagram
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
Jenkins: successfully running


3. Login by accessing the 8080 port on the server. The address to login my jenkins is: http://ec2-54-87-219-165.compute-1.amazonaws.com:8080, which is allowed in the security group.

4. Create Multi-Branch pipeline: If the project has multiple branches, this enables automatic CI/CD for each branch. 
5. Add one branch source created in github. Once code commits to the added branch and the repository, it will trigger the test and build automatically. 
6. Build successfully
7.  Check the stages for this build, it has scm stage, test stage and build stage in pipeline. 

	a. Checkedout SCM: performs the function of CI, it will retrieve the latest version of code in the source version control system continuously. Manage the latest change tracked from my GitHub Retail-bank repository in this workload.
	
	b. Build Stage: Compile the code that was retrieved. If there’s any error in the source code or configuration problems, build cannot get through.
	
	c. Test stage: this is also one stage in Jenkins CI/CD that enables continuously run tests to validate the code.
	
	d.These three steps ensure that we can quickly get, build and test the program before deploying. 
	
### Elastic beanstalk
1. Create two service roles, one for Elastic Beanstalk and one for EC2. Each role has their own permissions. After these roles are created, they can be used later to gain permissions.
2. Create an “Environment” in AWS elastic beanstalk. This environment will provide the required permissions to access services by adding created two roles before, running platform.
3. Before the EBS successfully created, I met the following error. By looking at the error message, to uncheck the Activated box, the program deployed successfully.
### Accessing web page
1. Click on the domain, which will translate to the IP address of the EC2 instance. Normally, we can access the resource. However, I got a 502 Bad Gateway error, indicating a server issue. With the hint, I found that the file I ‘ve uploaded is not right. And it caused the server to not run the application successfully. Before that I checked the Nginx error log and found error messages saying the connection is refused. As the following pictures. 

##Optimization
##Conclusion



