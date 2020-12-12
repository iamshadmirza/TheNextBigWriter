Creating REST API Using NodeJS, ExpressJs, MongoDB, And Mongoose

Hello Everyone 

My Name is  Minhaj Ahmad khan and I'm a Front-end developer. This is my first blog where I create a REST API using NodeJS, ExpressJs, MongoDB, and Mongoose. I'm super excited to let's get started.


 A REST API (also known as RESTful API) is an application programming interface that conforms to the constraints of REST architecture. REST stands for representational state transfer. Application programming interfaces (APIs) are everywhere. It is a software that allows two applications to communicate with each other over the internet and through various devices. Every time you access an app like Instagram or check the weather on your smartphone, an API is used. 


So let’s start and write some Javascript and build a RESTful API in Node.js.

**Requirements**

Node.js

Express.JS

MongoDB

Mongoose (connect our back end to a MongoDB database)

Postman (Postman is a great tool when trying to dissect RESTful APIs made by others or test ones you have made yourself. )

**Installation**
1.  Install node(if you have already  node on your machine then skip this step) 
2.  Install MongoDB (if you have already  MongoDB  on your machine then skip this step)
3.  Let's create a repository called **RestfulAPI** 
4.  Open **RestfulAPI** repository on command line terminal
5.  
```npm init -y  
```  initializing our project 

Now we can see the **package.json** file which will include all of the project’s packages we need to run our API.

###  Installing Express
Express is a fast, assertive, essential, and moderate web framework of Node.js that helps manage a server and routes.

Let's install Express with node 

6.
```npm install express```

### installing Mongoose 
Mongoose is a way to make a connection with the MongoDB database. It provides MongoDB validation and query in a very simple manner and it makes development fast.

Let's install Mongoose with node

7.
```npm install mongoose```

**Install nodemon** 

nodemon is a tool that helps develop node. js based applications by automatically 

restarting the node application when file changes in the directory are detected.



8.
``` npm install nodemon```



We now have everything needed to start building our  API.

We are going to create API which maintains student record with the help of API we can perform create read update and delete (CURD) Operation.



Let's write some javascript that will initialize and define endpoints in app.js
avoid **get()** we discuss after a while.




```
const express = require('express');
const app = express();
const port = process.env.PORT || 3000 ;

app.get('/', (req,res)=>{

      res.send('<h1>this is home page of Student Api </h1>')
})

app.listen(port , ()=>{
    console.log(`connection is  extablished`)
});
```
require express now we got express as a function and create new constant with the help of express for use express method and properties.

listen() method creates a listener on the specified port or path.




Let's run this code  ``` nodemon src/app.js``` and what happened 








![Screenshot (761).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607604127311/lYlNVcPr5.png)

 Cool!  the connection is established let's move forward  

Let's connect MongoDB with mongoose
for that, we need to create a folder and file inside src folder ```src/database/connection.js ``` where write some javascript code to connect to MongoDB to the mongoose.

```
const mongoose = require("mongoose");
let url = process.env.DATABASE_URL || "mongodb://localhost:27017/students-record";
mongoose.connect(url, {
    useCreateIndex: true,
    useNewUrlParser: true,
    useUnifiedTopology: true
}).then(() => {
    console.log('connection successful')
}).catch((e) => {
    console.log(`connection unsuccessful ${e}`)
})
```
We can connect to MongoDB with the mongoose.connect() method.

```mongoose.connect('mongodb://localhost:27017/students-record', {useNewUrlParser: true,useCreateIndex: true,useUnifiedTopology: true});```

This is the minimum needed to connect the students-record database running locally on the default port (27017).
after that, we need to call the connect function with the help of mongoose where we pass URL and a call back function that returns a promise. to avoid
deprecation Warnings set ```useCreateIndex: true,
  useNewUrlParser: true,
  useUnifiedTopology: true```
 

We need to require **connection.js** in our express file **(app.js) **   ```require('./database/connection')```

```
const express = require('express');
const app = express();
const port = process.env.PORT || 3000 ;

require('./database/connection')

app.post('/studentregistration', (req,res)=>{

      res.send('<h1>this is home page of Student Api </h1>')
})

app.listen(port , ()=>{
    console.log(`connection is  extablished`)
});
```

Now run ** app.js** file and see what happened 



![Screenshot (765).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607606304478/TJXDTRO0j.png)

Cool! database connection successful 


Now let's define our database schema for that we need to create a folder and file inside src  **src/model/studentschema.js**. to know more about schema read  [official document here ](https://mongoosejs.com/docs/guide.html#definition) 

```

const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
        minlength: 3,
    },
   class : {
      type:String,
    },
    email: {
        type: String,
        required: true,
        unique: true,

    },
    phone: {
        type: Number,
        required: true,
        maxlength: 10,
        minlength: 10
    },
    address: {
        type: String,
        required: true,
    }
})

const student = new mongoose.model('student', studentSchema)

module.exports = student;

``` 

after defining schema we defined collection(table) with the help of a ```mongoose.model``` method and pass collection name ```student``` and schema name ```studentSchema``` then exports this collection because we need to use in **app.js** file.



```
const express = require('express');
const app = express();
const port = process.env.PORT || 3000 ;
const student = require('./model/studentschema')
require('./database/connection')


app.post('/studentregistration', (req,res)=>{

      res.send('<h1>this is home page of Student Api </h1>')
})

app.listen(port , ()=>{
    console.log(`connection is  extablished`)
});
``` 
cool! database connected, the schema defined properly everything is going good let's move the second part of our blog which is create, read, update, delete  (CURD) operation. 




### Now let’s begin with the POST method.

The POST method sends data to the server.  [know more about POST method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) 
```
const express = require('express');
const app = express();
const port = process.env.PORT || 3000 ;
const student = require('./model/studentschema')
app.use(express.json())
require('./database/connection')

app.post('/student-registration', (req, res) => {
    const user = new student(req.body)
    user.save().then(() => {
        res.status(201).send(user)
    }).catch((e) => {
        res.status(400).send(e)
    })
})

app.listen(port , ()=>{
    console.log(`connection is  extablished`)
});


```

This method will accept **name, class, email, phone, address** from the ```req.body```

POST method takes two parameters so we passed **root** and  **callback function**.
the callback function has two parameters req and res. By using ```req.body```  we are fetching data from the body and store in our collection(table) by ```save()```.

**Let's test our post API using postman 
**




![post.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607765551193/g5xsdueP4.png)

Wow, it's working fine data successful store in our collection.

### Next, let’s create a GET method.

This method will return All Student records.  [know more about GET method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) 

Now let’s  create a router with our first GET method:

```
const express = require('express');
const app = express();
const port = process.env.PORT || 3000 ;
const student = require('./model/studentschema')
app.use(express.json())
require('./database/connection')

app.get('/show-student-record', async (req, res) => {
    try {
        const showStudentData = await student.find()
        res.status(200).send(showStudentData)
    } catch (e) {
        res.status(400).send(e)
    }
})

app.listen(port , ()=>{
    console.log(`connection is  extablished`)
});

```
```.find()``` return all the student records from student.if the student record cannot be found, the method returns the error message and status code 404 record not found

 ** Let's test our post API using postman **



![get.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607765995286/Veq0OISv7.png)

It's working perfectly fine we can see all records in our database 



### Now for updating a Student record  with a PATCH method 
PATCH method can be used to update partial resources. For instance, when you only need to update one field of the resource.  [know more about PATCH method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) 

```
app.patch('/student-record-update/:id', async (req, res) => {
    try {
        const _id = req.params.id;
        const studentUpdate = await student.findByIdAndUpdate(_id, req.body, {
            new: true
        })
        res.status(200).send(studentUpdate)
    } catch (e) {
        res.status(400).send(e)
    }
})
```

functions need an element called ObjectID to be able to tell the database which specific element you want to update. ObjectID created automatically when we insert a new record into your database after that we are adding an ObjectId in the URL then we require ObjectID from a URL  like this                  ```   const _id =req.params.id;```.
after that  ```findByIDAndUpdate()```  where the first parameter is ```_id ``` and the second is the data that we are updating  ```req.body```.``` {new:true} ``` update student collection immediate

** Let's test our  API  using the PostMan **

Before updating student record



![before update.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607770690134/J_lYm0S64.png)

After updating student record



![after update.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607770706984/IJU9rgg9r.png)


###  Finally let’s create a DELETE method to remove the student record 

```
app.delete('/student-record-delete/:id', async (req, res) => {
    try {
        const _id = req.params.id
        const deleteRecord = await student.findByIdAndDelete(_id)
        res.status(200).send(deleteRecord)
    } catch (e) {
        res.status(400).send(e)
    }
})
```
functions need an element called ObjectID to be able to tell the database which specific element you want to delete. it's very similar to a patch request instead of ```findByIdAndUpdate``` we are using find ```findByIdAndDelete``` where we are passing _id in both arguments like this ```findByIdAndDelete({_id:_id})``` we know that key and value are same so we write like this ```findByIdAndUpdate```.

**Let's test our API  **

Before deleting  student record 

![before delete.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607771891361/idFsEKGmm.png)

After deleting  student record 




![after delete.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1607771906081/6Fpcp8CLZ.png)

That's it, I hope it was helpful to you. Thanks for reading.


**Minhaj ahmad khan**


 





