# (STEP 5) - PROJECT 3 : MERN STACK IMPLEMENTATION.


## STEP 1 - BACKEND CONFIGURATION.


Update ubuntu

`sudo apt update`


![Update Ubuntu](./Images/Update%20Ubuntu.PNG)


Upgrade ubuntu


`sudo apt upgrade`


![Ubuntu Upgrade](./Images/Ubuntu%20Upgrade.PNG)


Lets get the location of Node.js software from Ubuntu repositories.


`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`


![Node.js Location](./Images/Node.js%20Location.PNG)


**Install Node.js on the server**


Install Node.js with the command below.


`sudo apt-get install -y nodejs`


![Install Node.js](./Images/Install%20Node.js)


**Note:** The command above installs both *nodejs* and *npm.* NPM is a package manager for Node like *apt* for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

Verify the node installation with the command below.


`node -v`


![Node Verification](./Images/Node%20Verification.PNG)



Verify the npm installation with the command below.


`npm -v `


![NPM Verification](./Images/NPM%20Verification.PNG)


**Application Code Setup**


Create a new directory for your To-Do project:


`mkdir Todo`


![Create Todo Directory](./Images/Create%20Todo%20Directory.PNG)


Run the command below to verify that the Todo directory is created with ls command.


`ls`


![Verify Todo Directory](./Images/Verify%20Todo%20Directory.PNG)



**TIP:** 
In order to see some more useful information about files and directories, you can use following combination of keys *ls -lih* – it will show you different properties and size in human readable format. You can learn more about different useful keys for *ls* command with *ls --help.*


Now change your current directory to the newly created one:


`cd Todo`


![Directory Change Todo](./Images/Directory%20Change%20Todo.PNG)


Next, you will use the command *npm init* to initialise your project, so that a new file named *package.json* will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press *Enter* several times to accept default values, then accept to write out the *package.json* file by typing *yes.*



`npm init`


![Initialise Project_Package.json](./Images/Initialise%20Project_Package%2Cjson.PNG)



Run the command ls to confirm that you have package.json file created.

`ls`

![Confirm Package.json Created](./Images/Confirm%20Package.json%20Created.PNG)



Next, we will Install ExpressJs and create the Routes directory.


**INSTALL EXPRESSJS**

*Remember that Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.*

To use express, install it using npm:


`npm install express`


![Install Express](./Images/Install%20Express.PNG)


Now create a file index.js with the command below.


`touch index.js`


![Create index.js](./Images/Create%20index.js)


Run ls to confirm that your index.js file is successfully created.


`ls`


![Confirm index.js](./Images/Confirm%20index.js)



Install the dotenv module.


`npm install dotenv`


![Install dotenv](./Images/Install%20dotenv.PNG)


Open the index.js file with the command below.


`vim index.js`


Copy and paste the code below into the file. Use i to instert and then paste.


```
const express = require('express');
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
});
```

To save and quick follow the steps below.

*  Esc
*  Shift + : then Enter
*  Wq t(It will show this :wq) then Enter.


![Save_Quit index.js](./Images/Save_Quit%20index.js)




To confirm the content of the file run the command below.


`cat index.js`


![Confirm index.js_2](./Images/Confirm%20index.js_2.PNG)



Notice that we have specified to use port *5000* in the code. This will be required later when we go on the browser.


Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:



`node index.js`

![Server Running](./Images/Server%20Running.PNG)


Now we need to open this port in EC2 Security Groups. Refer to Project 1 Step 1 – Installing the Nginx Web Server. There we created an inbound rule to open TCP port 80, you need to do the same for port 5000, like this:



1. Go to the instance
2. Select Security
3. Click on Security Group link under Security Group
4. Click on Edit Inbound Rules
5. Click Add Rule
6. Fill the selections as shown below.

        Type = Custom TCP
        Port Range = 5000
        Source = Custom / 0.000/
        Description = Port 5000 for Project MERN To do application deployment.

7. Save Rules


![Edit Inbound Rules](./Images/Edit%20Inbound%20Rules.PNG)


Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:


http://PublicIP-or-PublicDNS:5000


In our case see below using the public address.


http://18.223.235.121:5000


**Quick reminder how to get your server’s Public IP and public DNS name:**
1) You can find it in your AWS web console in EC2 details
2) Run curl -s http://169.254.169.254/latest/meta-data/public-ipv4 for Public IP address or 

3) Run curl -s http://169.254.169.254/latest/meta-data/public-hostname for Public DNS name



![Servber Browser Access](./Images/Server%20Browser%20Access.PNG)



**Routes**

There are three actions that our To-Do application needs to be able to do:

1. Create a new task
2. Display list of all tasks
3. Delete a completed task

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.


Note : Dont close the current terminal. Just click the + to open another window. Make sure you go back to Todo directory by using *cd Todo.*

![Directory Change Todo_2](./Images/Directory%20Change%20Todo_2.PNG)


For each task, we need to create routes that will define various endpoints that the *To-do* app will depend on. So let us create a folder *routes.*


`mkdir routes`


![Create routes Directory](./Images/Create%20routes%20Directory.PNG)


Change directory to routes folder.


`cd routes`


![Change To routes Directory](./Images/Change%20To%20routes%20Directory.PNG)


Now, create a file api.js with the command below.


`touch api.js`


![Create api.js](./Images/Create%20api.js)



Open the file with the command below.


`vim api.js`



Copy and paste the below code in the file. 


```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```

Use *i* to insert. Paste and then save by Esc then Shift + :
Then wq and Enter (It will appear like :wq)



![api.js file](./Images/api.js%20file.PNG)


Moving forward let create Models directory.


## MODELS

*Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.*

*A model is at the heart of JavaScript based applications, and it is what makes it interactive.*

*We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document.*


*In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties.*

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

Change directory back Todo folder with cd ..


`cd ..`

![Change Directory Todo](./Images/Change%20Directory%20Todo.PNG)


Install Mongoose.


`npm install mongoose`


![Install Mongoose](./Images/Install%20Mongoose.PNG)



Create a new folder models :


![Create models folder](./Images/Create%20models%20folder.PNG)


Change directory into the newly created ‘models’ folder with the command below.



`cd models`


![Directory Change models](./Images/Directory%20Change%20models.PNG)



Inside the models folder, create a file and name it todo.js.


`touch todo.js`


![todo.js file](./Images/todo.js%20file.PNG)


**Tip:** *All three commands above can be defined in one line to be executed consequently with help of && operator, like this: Do not perform the below steps as you have already performed them above.*


`mkdir models && cd models && touch todo.js`


Run ls to confirm the file was created.

`ls`


![Confirm todo file](./Images/Confirm%20todo%20file.PNG)



Open the file created with vim todo.js then paste the code below in the file:


`vim todo.js`

```
const mongoose = require('mongoose');
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

module.exports = Todo;
```


Save and exit using :wq

Confirm that you can see the file using the command below.


`cat todo.js`

![Update todo.js](./Images/Update%20todo.js)



Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, open *api.js* with *vim api.js*, delete the code inside with :%d command and paste there code below into it then save and exit.

Note to get to routes directory use *cd ..* to go back and the *cd routes.* as shown below.

  * `cd ..`

  * `cd routes`


![Directory Change routes](./Images/Directory%20Change%20routes.PNG)


In Routes directory, open *api.js* with

`vim api.js`


Delete the code inside with *:%d* command. 


![Delete api.js](./Images/Delete%20api.js)


Copy and paste the code below into it then save and exit.



![New Code api.js](./Images/New%20Code%20api.js)



The next piece of our application will be the MongoDB Database.




## MONGODB DATABASE



*We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up here. Follow the sign up process, select AWS as the cloud provider, and choose a region near you.*

https://www.mongodb.com/atlas-signup-from-mlab

Complete a get started checklist.

Click on Build a Database .


![Build Database](./Images/Build%20Database.PNG)


Select the free and shared option by clicking Create.


![Free Shared Option](./Images/Free%20Shared%20Option.PNG)


Select AWS as the Cloud provider, reccomended region as N. Virginia (us-east-1) and click Create Cluster.


![Create Cluster](./Images/Create%20Cluster.PNG)



A Quickstart page will be displayed. *Your cluster has finished provisioning* will be displayed at the bottom when done.


![Quick Start](./Images/Quick%20Start.PNG)


Click on *All Clusters* at the top right.


![All Clusters](./Images/All%20Clusters.PNG)



Click on the name of the cluster. In our case it is Cluster0.


![Cluster0](./Images/Cluster0.PNG)



The screen below will be displayed after opening Cluster0.


![Cluster0 Display](./Images/Cluster0%20Display.PNG)



Click on Database Access and select on *Add New Database User*.


![Add New Database user](./Images/Add%20New%20Database%20User.PNG)


Under password, create a user and a password.

Jakabondo_PBL3
PassxWord_3


![Credentials](./Images/Credentials.PNG)


Leave everything as defaulted and move to the bottom and change the temporary user duration from 6 hours to 1 week. Then click on add user.



![Temporary User Duration](./Images/Temporary%20User%20Duration.PNG)



The screen below will show that the new database user has been added.



![Database User Added](./Images/Database%20User%20Added.PNG)


Select on Network Access to allow IP access from anywhere. Click AddIP Address.



![AddIP Address](./Images/AddIP%20Address.PNG)


Select "ALLOW ACCESS FROM ANYWHERE". Make sure you change the time of deleting the entry from 6 Hours to 1 Week then Confirm.



![Add IP Access List Entry](./Images/Add%20IP%20Address%20List%20Entry.PNG)


The screen belown will be generated.


![Add IP Access List Entry Output](./Images/Add%20IP%20Address%20List%20Entry%20Output.PNG)


Create a MongoDB database and collection inside mLab. Click on All Clusters and select Cluster0 then click on Collections.


![Collections](./Images/Collections.PNG)


Click on Add My Own Data.


![Add My Own Data](./Images/Add%20My%20Own%20Data.PNG)


Input the Database Name and Collection Name of your choice and then click Create.

    Database Name : JakabondoDB
    Collection Name : JakabondoC



![Create Database_JakabondoDB](./Images/Create%20Database_JakabondoDB.PNG)


In the *index.js* file, we specified *process.env* to access environment variables, but we have not yet created this file. So we need to do that now.

Create a file in your Todo directory and name it *.env.*


`touch .env`


![Create .env file](./\/Images/Create%20.env%20file.PNG)



Open the file using the command below.


`vi .env`

![Open .env file](./Images/Open%20.env%20file.PNG)


Add the connection string to access the database in it, just as below:


DB = 'mongodb+srv://username:password@network-address/dbname?retryWrites=true&w=majority'



Ensure to update *username*, *password*, *network-address* and *database* according to your setup.

To get most of the information, follow the steps below;

  * Click on All Clustors
  * Click on Clustor0
  * Overview and Click on Connect.


![Connect](./Images/Connect.PNG)



Click on Connect your application.


![Connect your application](./Images/Connect%20your%20application.PNG)

![Connect your application output](./Images/Connect%20your%20application%20output.PNG)


Copy the link;


mongodb+srv://Jakabondo_PBL3:password@cluster0.aptqxvm.mongodb.net/?retryWrites=true&w=majority

Take the information you received and edit the original link provided .


DB = 'mongodb+srv://Jakabondo_PBL3:PassWord_3@cluster0.aptqxvm.mongodb.net/JakabondoDB?retryWrites=true&w=majority'



Copy the link above and paste it in to the .env file. Use i to insert . Paste, esc and :wq to save and quit.



![Connections .env file](./Images/Connections%20.env%20file.PNG)



Run the command below to confirm the changes.


`cat .env`



![Confirm .env](./Images/Confirm%20.env.PNG)



*Now we need to update the **index.js** to reflect the use of **.env** so that Node.js can connect to the database.*

First, run the command below to confirm the path.

`ls`


![Confirm Path](./Images/Confirm%20Path.PNG)


Run the command below to open the file.


`vi index.js`


![Open index.js file](./Images/Open%20index.js%20file.PNG)



*Simply delete existing content in the file, and update it with the entire code below.*

To do that using vim, follow below steps

  * Open the file with vim index.js
  * Press i
  * Press esc
  * Type :
  * Type %d
  * Hit ‘Enter’


![Delete Contents index.js](./Images/Delete%20Contents%20index.js)


The entire content will be deleted.

then,

Press i to enter the insert mode in vi
Now, paste the entire code below in the file.Save and quit using esc, :wq then enter.



![New Code index.js](./Images/New%20Code%20index.js)



Run the code below to confirm the changes.

`cat index.js`


![Confirm index.js_3](./Images/Confirm%20index.js_3.PNG)



Using environment variables to store information is considered more secure and best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the index.js application file.

Start your server using the command:

`node index.js`

You shall see a message ‘Database connected successfully’, if so – we have our backend configured. Now we are going to test it.



![Database Connected Successfully](./Images/Database%20Connected%20Successfully.PNG)



## Testing Backend Code without Frontend using RESTful API

So far we have written backend part of our *To-Do* application, and configured a database, but we do not have a frontend UI yet. We need ReactJS code to achieve that. But during development, we will need a way to test our code using RESTfulL API. Therefore, we will need to make use of some API development client to test our code.

In this project, we will use Postman to test our API.

Install Postman and download on your machine.

Click the link below to learn how perform CRUD operartions on Postman.

https://www.youtube.com/watch?v=FjgYtQK_zLE


*You should test all the API endpoints and make sure they are working. For the endpoints that require body, you should send JSON back with the necessary fields since it’s what we setup in our code.*


Open Postman.


![Open Postman](./Images/Open%20Postman.PNG)


We now need to create a POST request to the API http://PublicIP-or-PublicDNS:5000/api/todos.

This request sends a new task to our To-Do list so the application could store it in the database.


Click the + at the top to create a new request.

![Create Request](./Images/Create%20Request.PNG)

Change to *Post*. and input the url below next to *Post*

http://PublicIP-or-PublicDNS:5000/api/todos. 

In our case it using thePublic IP it is;

http://3.143.212.245:5000/api/todos. 

**Note:** make sure your set header key *Content-Type* as *application/json*.


![Post](./Images/Post.PNG)


Select Body and Raw and type;
```
{
  "action" : "Working on Project 3" 
}
```

Then click on Send.


![Send Post](./Images/Send%20Post.PNG)


The output below will be displayed.


![Send Post Output](./Images/Send%20Post%20Output.PNG)



Create a GET request to your API on http://PublicIP-or-PublicDNS:5000/api/todos. This request retrieves all existing records from out To-do application (backend requests these records from the database and sends it us back as a response to GET request).



Click the + sign next to the POST request you just created for a new session.


![GET Request](./Images/GET%20Request.PNG)



Grab the url from the POST request and paste it next to GET.

Set header key *Content-Type* as *application/json*

Click Send.



![Send GET Request](./Images/Send%20GET%20Request.PNG)



![GET Request Output](./Images/GET%20Request%20Output.PNG)



**Optional task:** Try to figure out how to send a DELETE request to delete a task from out To-Do list.

**Hint:** To delete a task – you need to send its ID as a part of DELETE request.

*By now you have tested backend part of our To-Do application and have made sure that it supports all three operations we wanted:*

* Display a list of tasks – HTTP GET request
* Add a new task to the list – HTTP POST request
* Delete an existing task from the list – HTTP 
DELETE request

*We have successfully created our Backend, now let go create the Frontend.*



## STEP 2 - FRONTEND CREATION



Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. 

To start out with the frontend of the To-do app, we will use the `create-react-app` command to scaffold our app.

In the same root directory as your backend code, which is the Todo directory, open a new Termional session and run:



`npx create-react-app client`


Click y when prompted to proceed.


![Create react app client](./Images/Create%20react%20app%20client.PNG)



This will create a new folder in your *Todo* directory called *client,* where you will add all the react code.

**Running a React App**

Before testing the react app, there are some dependencies that need to be installed.

1. Install *concurrently.* It is used to run more than one command simultaneously from the same terminal window.

    `npm install concurrently --save-dev`


   ![Install Concurrently](./Images/Install%20Concurrently.PNG)


2. Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.


    `npm install nodemon --save-dev`


    ![Install nodemon](./Images/Install%20nodemon.PNG)


3. In *Todo* folder open the *package.json* file. Change the highlighted part of the below screenshot and replace with the code below.


```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
```


![Package.json file highlighted](./Images/Package.json%20file%20highlighted.PNG)



Run the command below to view package.json file.

`ls`


![View package.json location](./Images/View%20package.json%20location.PNG)



Open package,json file using the command below.


`vi package.json`


![Open package.json](./Images/Open%20package.json)



Edit the file as mentioned above with the new code.

Note: Use i to insert. Make the changes and the Save the file and quit with esc then :wq.


![Package.json code changes](./Images/Package.json%20code%20changes.PNG)


Run the command below to view the changes.


`cat package.json`


![View Edited package.json](./Images/View%20Edited%20package.json)



**Configure Proxy in package.json**

1. Change directory to ‘client’.


   `cd client`

   ![Directory Change Client](./Images/Directory%20Change%20Client.PNG)


   Run `ls` to confirm.


   ![View Directory Change](./Images/View%20Directory%20Change%20Client.PNG)



  2. Open the package.json file.


     `vi package.json`

     ![Open package.json_2](./Images/Open%20package.json_2.PNG)


  3. Add the key value pair in the package.json file "proxy": "http://localhost:5000".

      The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos

      Note: Follow the below steps to perform the above instructions.

      * Copy the link below;

        "proxy": "http://localhost:5000"

      * In the package.json file, click i to insert.

      * Paste the link and Save by esc the :wq

        ![Edited package.json file](./Images/Edited%20package.json%20file.PNG)


      * View edited file.

        ![View Edited package.json file_2](./Images/View%20Edited%20package.json%20file_2.PNG)



Now, ensure you are inside the Todo directory by running the command below.

`cd ..`


![Directory Change Todo_3](./Images/Directory%20Change%20Todo_3.PNG)


Run the command below.

   
`npm run dev`


![npm run dev](./Images/npm%20run%20dev.PNG)


Your app should open and start running on localhost:3000

In our case it it;

18.219.85.44:3000

The browser will be displayed running as shown below.


![App.js](./Images/App.js)



Important note: In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2 by adding a new Security Group rule. You already know how to do it.

Creating your React Components
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component.


From your Todo directory run


`cd client`


![Directory Change Client_2](./Images/Directory%20Change%20Client_2.PNG)


Move to the src directory.


`cd src`


![Directory Change src](./Images/Directory%20Change%20src.PNG)



Inside your src folder create another folder called components.


`mkdir components`


![Create components folder](./Images/Create%20components%20folder.PNG)


Move into the components directory with;

`cd components`


![Directory Change components](./Images/Directory%20Change%20components.PNG)



Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.


`touch Input.js ListTodo.js Todo.js`


![Create 3 files](./Images/Create%203%20files.PNG)


Open Input.js file.


`vi Input.js`


Copy and paste the following.

```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
```



View Input.js with the copied code using 

`cat Input.js`


![View Input.js](./Images/View%20Input%2Cjs.PNG)



![View Input.js_2](./Images/View%20Input.js_2.PNG)



To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.

Move to the src folder;

`cd ..`


![Directory Change src_2](./Images/Directory%20Change%20src_2.PNG)



Move to clients folder.

`cd ..`


![Directory Change Client_3](./Images/Directory%20Change%20Client_3.PNG)


Install Axios.


`npm install axios`



![Install axios](./Images/Install%20axios.PNG)


## FRONTEND CREATION (CONTINUED)


Go to ‘components’ directory.


`cd src/components`


![Directory Change components](./Images/Directory%20Change%20components_2.PNG)



After that open your ListTodo.js.


`vi ListTodo.js`


in the *ListTodo.js* copy and paste the following code;



```
import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

return (
<ul>
{
todos &&
todos.length > 0 ?
(
todos.map(todo => {
return (
<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
)
})
)
:
(
<li>No todo(s) left</li>
)
}
</ul>
)
}

export default ListTodo
```

Save and quit using :wq!

![New Code ListTodo](./Images/New%20Code%20ListTodo.PNG)



Then in your Todo.js file you write the below code.

Run `vi Todo.js` to open the file.

```
import React, {Component} from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {

state = {
todos: []
}

componentDidMount(){
this.getTodos();
}

getTodos = () => {
axios.get('/api/todos')
.then(res => {
if(res.data){
this.setState({
todos: res.data
})
}
})
.catch(err => console.log(err))
}

deleteTodo = (id) => {

    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if(res.data){
          this.getTodos()
        }
      })
      .catch(err => console.log(err))

}

render() {
let { todos } = this.state;

    return(
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos}/>
        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
      </div>
    )

}
}

export default Todo;
```


![New Code Todo.js](./Images/New%20Code%20Todo.js)



We need to make little adjustment to our react code. Delete the logo and adjust our App.js to look like this.

Move to the src folder.

`cd ..`


![Directory Change src_3](./Images/Directory%20Change%20src_3.PNG)



Make sure that you are in the src folder and run;


`vi App.js`


Delete the contents of the file by following the steps below;

* Press i
* Esc
* :%d (Shift : will help you get :)
* Enter


![Delete App.js Contents](./Images/Delete%20App.js%20Contents.PNG)



Copy and paste the code below into it.


```
import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}

export default App;
```


![Changes App.js](./Images/Changes%20App.js)


After pasting, exit the editor.

In the src directory open the *App.css*


`vi App.css`




![App.css contents](./Images/App.css%20contents.PNG)



Delete the existing code using;

`:%d`


Then paste the following code into App.css:


```
.App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
```

Save and exit using :wq!


![New Code App.css](./Images/New%20Code%20App.css)



In the src directory open the index.css;


`vim index.css`

Delete the existing code using the comand;

`%d`


![Delete index.css Contents](./Images/Delete%20index.css%20Contents.PNG)



Copy and paste the code below:


```
body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}
```

Save and quit.


![New Code index.css](./Images/New%20Code%20index.css)



Go to the Todo directory;


`cd ../..`


![Directory Change Toddo_4](./Images/Directory%20Change%20Todo_4.PNG)



When you are in the Todo directory run:


`npm run dev`



![Webpack Compiled Successfully](./Images/Webpack%20Compiled%20Successfully.PNG)





Assuming no errors when saving all these files, our To-Do app should be ready and fully functional with the functionality discussed earlier: creating a task, deleting a task and viewing all your tasks.


Get your IP Address from the and the screen below will be displayed when you seach the link through your browser.

localhost:3000

3.15.13.52:3000


![Todo App](./Images/Todo%20App.PNG)


You can add an item (Completed Project 3)as shown below.



![Completed Project 3](./Images/Completed%20Project%203.PNG)




In this Project #3 we have created a simple To-Do and deployed it to MERN stack. We wrote a frontend application using React.js that communicates with a backend application written using Expressjs. We also created a Mongodb backend for storing tasks in a database.









































