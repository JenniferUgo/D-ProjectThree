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

### Next we install ExpresJs and create the Routes directory

__
## INSTALL EXPRESSJS

### To use express, install it using npm, by running this commad:

>`npm install express`

![install express js](./images/install-expressjs.png)

### Next,  create a file index.js using this command:

>` touch index.js`

#### Verify the file has been created, using:

>`ls`

![verify index.js file creation](./images/verify-index.js.png)

### Next, Install the *dotenv* module, using this command:

>`npm install dotenv`

![install dotenv](./images/install-dotenv.png)

### Open the index.js file, using this command:

>`vim index.js`

#### And paste this:


>`const express = require('express');
require('dotenv').config();
const app = express();
const port = process.env.PORT || 5000;
app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});
app.use((req, res, next) => {
res.send('Welcome to Express');
});
app.listen(port, () => {
console.log(`Server running on port ${port}`)
});`

![paste in index.js file](./images/paste-in-indexjs-file.png)

#### *Click **esc**, then*,
#### Save with:

>`:w`

#### Exit with:

>`:qa`

### Next, we start the server to see if it works, using this command:

>`node index.js`

#### *If everything goes well, you should see **Server running on port 5000** in your terminal.* 

![like so](./images/server-running-on-port-5000.png)

### Now we need to open this port in EC2 Security Groups, Edit Inbound Rules and add rules.

![EDIT INBOUND RULES](./images/edit-inbound-rules.png)

### Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:

>`http://<PublicIP-or-PublicDNS>:5000`

#### If everything is correct, you should see ***Welcome to Express***

![welcome to express](./images/welcome-to-express.png)

-
####             ***Routes***
### Our To-Do application should be able to do the following

1. Create a new task
2. Display list of all tasks
3. Delete a completed task

#### Each task will be associated with some particular endpoint and will use different standard HTTP request methods: **POST, GET, DELETE**

### *We will create routes that will define various endpoints that the To-do app will depend on*.

### Create a ***routes*** folder, using this command:

>`mkdir routes`

![create routes dir](./images/mkdir-routes.png)

### Now, create a file api.js, using this command:

>`touch api.js`

![create api.js](./images/create-routes-plus-apijs.png)

### Open the api'js file, using:

>` vim api.Js`

### And paste this:

>`const express = require ('express');
const router = express.Router();
router.get('/todos', (req, res, next) => {
});
router.post('/todos', (req, res, next) => {
});
router.delete('/todos/:id', (req, res, next) => {
})
module.exports = router;`

![insert in api.js](./images/insert-in-apijs.png)

#### *Click **esc**, then*,
#### Save with:

>`:w`

#### Exit with:

>`:qa`

--- 
---
## MODELS

### Since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.

#### To create a Schema and a model, install mongoose into the Todo directory, using this command:
>`npm install mongoose`

![install mongoose](./images/install-mongoose.png)

### Next, create a new folder named ***models***, using this command:
>`mkdir models`

### Change directory to models:
>` cd models`

### Inside the models folder, create a file and name it ***todo.js***, using this command:

>` touch todo.js`

![create a file in models dir](./images/create-dir-and-file.png)

### Next, open the file created with `vim todo.js` command, then paste the code below in the file:

>`const mongoose = require('mongoose');
const Schema = mongoose.Schema;
//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})
//create model for todo
const Todo = mongoose.model('todo', TodoSchema);
module.exports = Todo;`

![vim todo.js](./images/vim-todojs.png)

### open api.js file using `vim api.js` cammand, delete what's in the file using `:&d` command, and replace with the following code:

>const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

>router.get('/todos', (req, res, next) => {

>//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

>router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

>router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

>module.exports = router;

![paste new code in api.js file](./images/paste-in-apijs.png)

