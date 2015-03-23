You may want to make prototypes that are more complex than simple HTML files. For example, you may want to respond to input from a form, and show different pages based on answers given by the user.

To do this you will need to create 'routes' - rules for the server to respond to certain URLs.

For example, with a route of `/sample` the URL is:

    http://localhost:3000/sample
    
All routes for the application are kept in the [routes.js](https://github.com/tombye/express_prototype/blob/master/routes.js) file. They follow this format:

    verb(route, callback(request, response) {
        response.render(template, data);
    });

Let's break this down into bits:

* **verb** : the type of request ('get' or 'post')
* **route** : the route section of the URL as explained above
* **callback** : a function that contains the code executed when that route is requested
* **request** : the 1st parameter sent to the callback, an object representing the HTTP request made
* **response** : the 2nd parameter sent to the callback, an object representing the HTTP response that will be sent
* **response.render** : method of the response object used to create a page to send back to the browser that made the request
* **template** : the 1st parameter sent to response.render, the name of the template file used to render the page, minus its `.html` extension
* **data** : the 2nd parameter sent to response.render, an object containing variables to send into the template

So as an example, a request for the URL `http://localhost:3000/sample` has this route:

    get('/sample', function(req, res) {
        res.render('sample', { 'assetPath' : '/public/' });
    });
    
We are saying that for a `get` request for the `/sample` route we should run the code:

    res.render('sample', { 'assetPath' : '/public/' });
    
This is the `render` method of the `res` parameter being run with the parameters:

1. the template called `sample`
2. the `{ 'assetPath' : '/public/' }` data object.

Template files are found this way: `/views/` + `template` parameter + `.html`. The `sample` template therefore points to the `/views/sample.html` file. 

In the same way, the template `/examples/hello_world` would point to the `/examples/hello_world.html` file.

[Read the Express documentation for routes](http://expressjs.com/3x/api.html#app.VERB)