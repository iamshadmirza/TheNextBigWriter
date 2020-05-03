## Login System using Node/Express

In this tutorial, I would walk you through how you can create a login system with node/express/mongodb using bcrypt to hash passwords and jwt (jsonwebtoken) for session management.

> Tech Stack: Node/Express/Ejs/MongoDB/BCrypt/JWT

Lets get started

Create a folder on Desktop as 'login-system' and initialize the project in there.

    cd Desktop
    mkdir login-system
    cd login-system
    npm init

Change the entry point as _server.js_ and author as _your name_

Now install the dependencies:

    npm install express ejs mongoose bcrypt jsonwebtoken

Also we need nodemon to restart the server whenever code is changed.

Once, these dependencies are installed, its time to create _server.js_ and

    touch server.js

Now, we need to initialize the server in here.

    const express = require('express');

    const app = express();
    const port = process.env.PORT || 5001;

    app.use(express.json());
    app.use(express.urlencoded({ extended: true }));

    app.get('/', async (req, res) => {
        res.send('Index Route')
    }

    app.get('/register', async (req, res) => {
        res.send('Register Route')
    }

    app.listen(port, console.log(`Server is running at port ${port}`));

In the root directory, create a db.js file, in this file we will connect the MongoDB database.

login-system/db.js

    const mongoose = require('mongoose');

    mongoose.connect(
        'mongodb://localhost:27017/login-system',
        { useNewUrlParser: true, useUnifiedTopology: true },
        console.log('Database Connected')
    );

Now we need to bring this file in server.js

login-system/server.js

    const db = require('./db');

We have our server running and database connected, it time to write some markup for login and register route.

We need to create a folder named 'views' in root directory.

login-system/views/index.ejs

    <html>
    <head>
        <title>Login System</title>
    </head>
    <body>
        <h1>Login Page</h1>
        <form action="/" method="post">
        <input type="email" placeholder="Email" name="email" />
        <input type="password" placeholder="Password" name="password" />
        <button>Login</button>
        </form>
        <a href="/register">Register</a>
    </body>
    </html>

login-system/views/register.ejs

    <html>
    <head>
        <title>Login System</title>
    </head>
    <body>
        <h1>Registeration Page</h1>
        <form action="/register" method="post">
        <input type="text" placeholder="Name" name="name" />
        <input type="email" placeholder="Email" name="email" />
        <input type="number" placeholder="Age" name="age" />
        <input type="password" placeholder="Password" name="password" />
        <button>Register</button>
        </form>
        <a href="/">Login</a>
    </body>
    </html>

We have both the views ready to render in respective routes, now we need to import ejs in server.js and set it as default view engine.

login-system/server.js

    const ejs = require('ejs');

    app.set('view engine', 'ejs');

Now in place of _res.send()_ we need to render views.

    app.get('/', async (req, res) => {
        res.render('index')
    }

    app.get('/', async (req, res) => {
        res.render('register')
    }

We need to make a User model for the database. Create a models folder in the root directory.

login-system/models/User.js

    const mongoose = require('mongoose');

    const userSchema = new mongoose.Schema({
    name: { type: String },
    email: { type: String },
    age: { type: Number },
    password: { type: String },
    dateRegistered: { type: Date, default: new Date() }
    });

    module.exports = user = mongoose.model('user', userSchema);

Now we need to import this model in _server.js_ in order to use it further.

login-system/server.js

    const User = require('./models/User');

For authentication purpose we need BCrypt and JWT in our _server.js_. Let's import it

login-system/server.js

    const bcrypt = require('bcrypt');
    const jwt = require('jsonwebtoken');

Now, we have to write code for registering the user. To register the user we need to make a POST request at /register

login-system/server.js

    app.post('/register', async (req, res) => {
    try {
        const { name, email, age, password } = req.body;
        const hashedPassword = await bcrypt.hash(password, 10);
        const user = new User({ name, email, age, password: hashedPassword });
        await user.save();
        res.send('User Registered');
    } catch (error) {
        console.log(error)
    }
    });

After registering the user we need to make a view for logged in users, lets call it dashboard view. We will show name, email and age dynamically here.

login-system/views/dashboard.ejs

    <html>
    <head>
        <title>Dashboard</title>
    </head>
    <body>
        <h1>Dashboard</h1>
        <ul>
        <li>Name: <%= name %></li>
        <li>Email: <%= email %></li>
        <li>Age: <%= age %></li>
        </ul>
        <br />
        <form action="/logout" method="post">
        <button>Logout</button>
        </form>
    </body>
    </html>

To login the user, we need to make a POST request at index route i.e. '/'

login-system/server.js

    app.post('/', async (req, res) => {
    try {
        const { email, password } = req.body;
        const user = await User.find({ email });
        if (user.length > 0) {
        const authResult = await bcrypt.compare(password, user[0].password);
        if (authResult) {
            const token = jwt.sign({ id: user[0]._id }, 'secretsecret', {
            expiresIn: '24h'
            });
            res.cookie('token', token);
            res.render('dashboard', {
            name: user[0].name,
            email: user[0].email,
            age: user[0].age
            });
        } else {
            res.send('Auth Failed');
        }
        }
    } catch (error) {
        res.send('Auth Failed');
    }
    });

Our index route renders login page, but we want if the user is logged in it render dashboard view. We need jwt for this.

login-system/server.js

    app.get('/', async (req, res) => {
    const tokenCookie = req.headers.cookie;
    if (tokenCookie != undefined) {
        const token = tokenCookie.split('=')[1];
        const decoded = jwt.verify(token, 'secretsecret');
        const user = await User.findById(decoded.id);
        res.render('dashboard', {
        name: user.name,
        age: user.age,
        email: user.email
        });
    }
    res.render('index');
    });

Similarly, we don't want logged in users to go to register route for this we need to edit our register route as well.

    app.get('/register', async (req, res) => {
    const tokenCookie = req.headers.cookie;
    if (tokenCookie != undefined) {
        const token = tokenCookie.split('=')[1];
        const decoded = jwt.verify(token, 'secretsecret');
        const user = await User.findById(decoded.id);
        res.redirect('/');
    }
    res.render('register');
    });

Now, we need to make a post request at '/logout' route to logout the user.

    app.post('/logout', (req, res) => {
    res.clearCookie('token');
    res.redirect('/');
    });

The full source code for this tutorial is available [here](https://github.com/akulsr0/login-system-express)

Thank You :)
