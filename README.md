node_notes
==========
For ind. study teacher + `.md` practice for me.

### Installation and Tooling

1. Download and install [Node](http://nodejs.org/download/)
2. Download and install [Git](http://git-scm.com/) if not yet installed
2. Download and install [MongoDB](http://www.mongodb.org/downloads)
   * You may need to create the directory `/data/db` at root (e.g. C:/ drive by default)  
3. After installing node, `npm` should be available as a command
   * Open Windows Powershell or shell of choice and create directory for project
   * **Optional**: It helps to have nix style commands available,
     which can be achieved by installing [ruby](http://rubyinstaller.org/downloads/)
     * Make sure the directory containing `ruby.exe` is in your path variable. In shell: `set path="%path%;ruby-folder"`
   * Once project directory is created, make it a git repository:
   * Navigate to project directory and run: `git init`
   * In the same directory, run: `npm install -g express`. This will install express available as a command.
   * In the same directory, run: `express`. This will generate a project skeleton at the current directory.
   * List the files in directory, you should see a bunch of generated files and one thats named `Package.json`, in this file, you should see bunch of dependencies. Usually, all your external dependencies would be defined here.
   * You must install the dependencies before you can use them. so run: `npm install`
   * From now on, any change to the dependencies will require you to run `npm install`
   * If successfully gone through the above, you should also see `app.js` in the same directory.
   * From the shell, run: `node app.js` and in browser<br/>navigate to the indicated port e.g: "localhost:port#"
   * Good time to commit:

            git add -A
            git commit -a -m "initial commit"

4.  Everytime you make a change in your application, you must re-run `node app.js`
    To avoid this, run `npm install -g nodemon` 
    This module willmonitor for changes in your project and serve them up accordingly.
    No need to keep on running `node app.js` everytime.
    Just run once when you sit down to work in your project directory: `nodemon app.js`
    * For more usage info: [Go here](https://github.com/remy/nodemon)

### Configuring and using Mongo

1. In `package.json` add

           "mongodb":"3.1.x",
           "mongoose":"*"
            
   to dependencies.
2. Then run `npm install`. This will download the node modules that will let you work with with mongo.
3. Open `app.js` it should look something like this:
   ```javascript
    var express = require('express')
      , http = require('http')
      , path = require('path');

    var app = express();
    // all environments
    app.set('port', process.env.PORT || 3000);
    app.set('views', __dirname + '/views');
    app.set('view engine', 'jade');
    app.use(express.favicon());
    app.use(express.logger('dev'));
    app.use(express.methodOverride());
    app.use(express.bodyParser());
    app.use(app.router);
    app.use(express.static(path.join(__dirname, 'public')));

    // development only
    if ('development' == app.get('env')) {
      app.use(express.errorHandler());
    }

    http.createServer(app).listen(app.get('port'), function(){
      console.log('Express server listening on port ' + app.get('port'));
    });
   ```
   The `requires` at the top are kind of like `imports/includes... etc.` 
   and you should notice that only the http, express, and path modules are being used in the code.
   The `app.use` function tells which middleware your app wil be using.
   Depending on the middleware, they may sometimes be order sensitive as you will see later on.
4. At the top, where the `requires` are, add
   ```javascript
   ...
   , mongo = require('mongodb')
   , mongoose = require('mongoose')
   ...
   ```
5. (Ignoring code organization) At the bottom of the code add the lines:
   ```javascript
    var mongoUri = 'mongodb://localhost/yourdb';
    mongoose.connect(mongoUri);

    var connection = mongoose.connection;
    connection.on('error', console.error.bind(console, 'connection err:'));
    connection.once('open', function(){
	    console.log('mongodb: success connect!');
    });

    var UserSchema = mongoose.Schema({
    	username: String,
    	password: String,
    });
    
    var User = mongoose.model('User', UserSchema);
   ```
   Replace `yourdb` with desired name. After the connecting to the database, you can now setup "schemas" to model your users.
   Here a simple user schema is defined. You can add other fields you see approriate, see [here](http://mongoosejs.com/docs/schematypes.html) for more info.
   The `mongoose.model` will bind the UserSchema to the User model (probably a seperate collection on mongo) and the crud methods are now available via the `User` variable.

### Routes
Think of routes like the 'c' in mvc. All the actions will be defined by routes.
1. Delete the files routes directory generated by express.
2. Add a `index.js` file. We will define routes here.
3. Start by adding the line
   ```javascript
   module.exports = function(app){};
   ```
   Remember those `require` calls?, it returns whatever `modules.export` was set to. In this case, a function that takes an `app` object.
   [MoreDetails](http://stackoverflow.com/questions/5311334/what-is-the-purpose-of-nodejs-module-exports-and-how-do-you-use-it)
   Now whenever the `./routes` module is required with `require('./routes')(app)`, if no js file is specified, it takes `index.js` by default.
   The app variable was defined in `app.js` and passed to the module which was just a function.
4. To add a route, in the function add the lines:
   ```javascript
   app.get('/', function(req, res) {
			res.send('<h1>Welcome to my app!</h1>');
	 });
   ```
   This is the index route, whenever you bring up your site in the browser, you should see this page first.
   GET requests use `app.get` and POST requests use `app.post`, etc.
   `res.send` sends the response, see [here](http://expressjs.com/api.html#res.send) for other stuff you can send in the response.
5. 
