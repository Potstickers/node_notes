node_notes
==========
For ind. study teacher + `.md` practice for me.

### Installation and Tooling

  1.  Download and install [Node](http://nodejs.org/download/)
  2.  Download and install [Git](http://git-scm.com/) if not yet installed
  2.  Download and install [MongoDB](http://www.mongodb.org/downloads)
      * You may need to create the directory `/data/db` at root (e.g. C:/ drive by default)  
  3.  After installing node, `npm` should be available as a command
      * Open Windows Powershell or shell of choice and create directory for project
      * **Optional**: It helps to have nix style commands available,  
        which can be achieved by installing [ruby](http://rubyinstaller.org/downloads/)
        * Make sure the directory containing `ruby.exe` is in your path variable:  
          In shell: `set path="%path%;ruby-folder"`
      * Once project directory is created, make it a git repository:
      * Navigate to project directory and run: `git init`
      * In the same directory, run: `npm install -g express`   
        This will install express available as a command.
      * In the same directory, run: `express`
        This will generate a project skeleton at the current directory.
      * List the files in directory, you should see a bunch of generated files  
        and one thats named `Package.json`, in this file, you should see bunch of dependencies.  
        Usually, all your external dependencies would be defined here.
      * You must install the dependencies before you can use them. so run: `npm install`
      * From now on, any change to the dependencies will require you to run `npm install`
      * If successfully gone through the above, you should also see `app.js` in the same directory.
      * From the shell, run: `node app.js` and in browser 
        navigate to the indicated port e.g: "localhost:port#"
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

  1. 
