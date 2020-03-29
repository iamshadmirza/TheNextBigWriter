## Middlewares in Express JS

It has been a long time since Node.js was released.It has now become an integral part of the JS Ecosystem. Any JS developer be it Frontend or Full Stack would probably be familiar with Node.js. Any one who has worked on Node would have also worked with Express JS.

Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. It basically helps you manage everything from routes to handling requests and views for your web application. It also supports an MVC style architecture for the applications.

### What are Middlewares

A middleware is just a function which takes request(req), response(res) and the next middleware function(next) as the arguments. These are the function which helps to intercept the incoming request, perform a specific task and pass the execution to next middleware or route handler or even they can end the request-response cycle by returning a response.

So,for example we can think of Auth Middleware, which works to authenticate the users. We need to authenticate all the routes which user should access only if he/she is loggedIn. So, we will be doing something like as below code snippet.

![Auth Middleware Code Snippet](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585473072/auth-middleware_olqs7j.svg).

So, as soon as any of the above routes will hit the server. It will be redirected to Auth Middleware to perform authentication.If the authentication is successful, middleware will call next() and now the control will go to respective controllers to perform their task. And if the authentication fails, middleware will end the request-response cycle by sending an error logic response.

![Auth middleware works](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585474199/auth-middleware-works_aujyh4.png)

source: [https://miro.medium.com/](https://miro.medium.com/)

### How Middleware Works

Any request on the Node Server will be accessed by all the middlewares in the request-response cycle in a sequential order. The line of order in which the middlewares are defined matters a lot.You can take it as that the **output** of first middleware is **input** of the second middleware for **request** and **response** object. A middleware take a 3rd argument which is the next middleware or the route function. If your middleware doesn't returns a response it should call next() to pass the control to the next middleware function otherwise the request will always be hanging in the application.

![what are middleware](https://qph.fs.quoracdn.net/main-qimg-78c4c87d1e7f41795801b4a49b721d6f)

source: [https://miro.medium.com/](https://miro.medium.com/)

### Types of Middlewares

There are many types of middlewares which are as follows:

###### Application Level Middleware

Any middleware which is bound with the express app using app.use() or app.METHOD( where METHOD can be any HTTP method - GET, POST, PUT, DELETE). This type of middlewares are generally used to perform common business logics such as user authentication, logging each request etc.

![app level middleware](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585390499/app_nzdavx.svg)

###### Router Level Middleware

A middleware which is bound to an instance of express.Router(). It works similar to the application level middleware. Generally, it comes in use if you want to divide your main application routes to separate modules and use middlewares.

![router level middleware](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585391535/router_eofwlb.svg)

###### Built In Middleware

Express JS itself provides multiple built-In middlewares such as express.json, express.static etc. These can be used based on the use case in the application. Such as a web app will need express.static to server all the static resources for the web-app.

The entire list of built-in can be found here: <https://github.com/senchalabs/connect#middleware>

![Built In Middlewarte](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585393645/builtIn_pc8rwv.svg)

###### Error Handling Middlewares

Express comes with a built-in error handler that takes care of any errors that might be encountered in the app. This default error-handling middleware function is added at the end of the middleware function stack.

If you pass an error to next() and you do not handle it in a custom error handler, it will be handled by the built-in error handler; the error will be written to the client with the stack trace. The stack trace is not included in the production environment.

One can write any number of custom error handling middlewares in an app. The custom middlewares are different with other middlewares in a way that it accepts 4 arguments and the first one being the err.

![Error Handling Middlewares](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585394962/error_xz2fgu.svg)

###### Third Party Middlewares

There are multiple third party middlewares which can be used in Express. These can be used based on the use case in the application. Such as to parse the request body, your application needs a body parser.

![Third Party Middlewarte](https://res.cloudinary.com/dyyr6kwla/image/upload/v1585393493/thirdparty_frfo5z.svg)

That’s all for now for this article. I have tried to share my knowledge of Express Middlewares, hoping to help others. Please comment your valuable suggestions and feedback.

[Dev.to](https://dev.to/mishraasoumyaa) | [Twitter](https://twitter.com/mishraaSoumya) | [LinkedIn](https://www.linkedin.com/in/mishraa-soumya/)
