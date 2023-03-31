# SIMPLE TO-DO APPLICATION ON MERN WEB STACK DOCUMENTATION

## We will implement a web solution based on MERN stack in AWS Cloud

### **MERN** Web stack consists of following components:

1. **M**ongoDB: A document-based, No-SQL database used to store application data in a form of documents.
2. **E**xpressJS: A server side Web Application framework for Node.js.
3. **R**eactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.
4. **N**ode.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.
### First, we need to do these steps:
1. Create an account on [AWS](https://aws.amazon.com/)
2. Create an instance (virtual machine) by selecting “ubuntu server 20.04 LTS” from Amazon Machine Image(AMI)(free tier).
3. Select “t2.micro(free tier eligible)”
4. On the security group and select “existing security group” review and click **Launch Instance**.
 #### This launches the instance and takes you to the Instances dashboard
 ![Launch instace](./images/launch-instance.png)

 5. Then open a terminal on your system and enter the folder where your previously downloaded PEM file is located.

 #### *In this case we use the Git Bash Terminal*
 ![cd downloads](./images/cd-downloads.png)

 #### 6. Connect to the instance from ubuntu terminal using this command:
 >`ssh -i "Jennee-EC2.pem" ubuntu@ec2-35-176-8-236.eu-west-2.compute.amazonaws.com`

 ![connect to instance](./images/connect-to-instance.png)


 #### *This automatically connects to the instance when you click Enter*
 ![connected to instance](./images/connected-to-instance.png)

 ## BACKEND CONFIGURATION
 ### First, we update ubuntu, using the command:
 >` sudo apt update`

 ![update ubuntu](./images/update-ubuntu.png)

 ### Them we upgrade ubuntu, using this command:
 >`sudo apt upgrade`

 ![upgrade ubuntu](./images/upgrade-ubuntu.png)

 ### Next, we get the location of Node.js software from Ubuntu repositories, using this command:
 >`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

 ![locate Nodejs](./images/nodejs-location.png)

 ### Then we Install Node.js on the server, using this command:
 >`sudo apt-get install -y nodejs`

 ![install Node.js](./images/install-nodejs.png)

 #### *The command above installs both **nodejs** and **npm**. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.*

 ### We verify the *node* installation with using this command:

 >`node -v`

 ![verify node.js](./images/verify-nodejs.png)

 ### Also Verify the *npm* installation with using this command:

>`npm -v`

![verify npm](./images/verify-npm.png)

#### **Application Code Setup**

### We create a ney directory for out To-Do project, using this command:

>`mkdir Todo`

#### Then verify the directory we created, using:
>`ls`

![create to-do directory](./images/create-directory.png)

### Next, we change current directory to the newly created one, usimg this command:

>` cd Todo`

### Next, we initialize the project so that a new file package.json will be created. This file contains information of the application and the dependencies it needs to run.

#### We initialize the project using this command:

>`npm init`

#### *Click **Enter** several times to continue, then sele **yes** to complete the process*

![initialise the project](./images/initialise-project.png)

### Verify that the package was created, using this command:

>`ls`

![verify package](./images/verify-package.png)

