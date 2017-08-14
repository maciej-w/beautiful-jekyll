---
layout: post
title: NodeJS as Windows Service
subtitle: Let's build a PDF Report builder using just NodeJS
bigimg: ../img/analog.jpg
---

### Recently I was given a task of writing a PDF Reporting solution. I ended up writing everything using Crystal Reports, due to business reliance
### But started with this NodeJS as Windows Service setup.

My thoughts on the setup:
- should be easy to update for 'future devs' so picked Javascript
- hould be easy to support so a Windows service sound like a good idea

As I like Node.js I started looking for modules and straight away found:
- handlebars-pdf module
- node-windows module

As you can expect the first one builds PDF reports and it's really easy to use especially when combined with mssql (module responsible
for connecting with MS SQL instances and running stored procs). The second one is able to run your Node.js as a Service! How cool is that!

I started with Node.js installation, this can be done using an executable file which can be downloaded from Node js website.

Then:
{% highlight shell %}
npm install express-generator -g
{% endhighlight %} 

Afterwards I generate an app with Pug template engine (I won't need it but just in case as default Jade is not supported anymore):
{% highlight shell %}
express --view=pug PDF_Reporting
{% endhighlight %} 

Then enter the directory:
{% highlight shell %}
cd PDF_Reporting
{% endhighlight %} 

Install node-windows according to the instructions:
{% highlight shell %}
npm install -g node-windows
{% endhighlight %} 
And:
{% highlight shell %}
npm link node-windows
{% endhighlight %} 

Node Windows is now installed! Let's create a Windows service:

Default Express setup is in the bin directory in the www file. Taking this into account we can create the install Service script service.js in the bin directory:

{% highlight javascript %}
var Service = require('node-windows').Service;

// Create a new service object
var svc = new Service({
  name:'PDF Reports',
  description: 'Runs node.js server building PDF Reports.',
  script: 'C:\\Users\\YOURUSERNAME\\Documents\\projects\\PDF_Reports\\bin\\www',
  env:{
    name: "NODE_ENV",
    value: "production"
  }
});

// Listen for the "install" event, which indicates the
// process is available as a service.
svc.on('install',function(){
  svc.start();
});

// Just in case this file is run twice.
svc.on('alreadyinstalled',function(){
  console.log('This service is already installed.');
});

// Listen for the "start" event and let us know when the
// process has actually started working.
svc.on('start',function(){
  console.log(svc.name+' started!\nVisit http://127.0.0.1:3000 to see it in action.');
});

// Install the script as a service.
svc.install();
{% endhighlight %} 

I open the VS Code Terminal, enter the bin directory and:

{% highlight shell %}
node service.js
{% endhighlight %} 

You can do the same by using Command Prompt or Powershell.

Go to Services and there it is, your own Windows Service running your app! Go to the browser and open localhost:3000 or http://127.0.0.1:3000 if you haven't changed the default port.

Now the fun part begins. Install handlebars-pdf using npm and add this script to app.js:

{% highlight javascript %}
//Add to dependencies
let pdf = require('handlebars-pdf')

// In the future you can add mssql and call stored procs here, we just create a PDF report every 1.5 seconds
function callSQLdb() {

  let document = {
      template: '<h1>{{msg}}</h1>'+
      '<p style="color:red">Red text</p>'+
      '<img src="https://archive.org/services/img/image" />',
      context: {
          msg: 'Hello world'
      },
      path: "./pdf/test-"+Math.random()+".pdf"
  }
   
  pdf.create(document)
    .then(res => {
        console.log(res)
    })
    .catch(error => {
        console.error(error)
    })

}

//We might have used a more complex solution, but we just want to call a SQL script which checks a column if it's null if yes it returns some stuff from that row so we can pass that to our report
setInterval(callSQLdb, 1500);

{% endhighlight %} 

OK. So I did all that and nothing! It works when you run it locally using node but not from the service... Luckily the node-windows module adds a daemon folder in the directory from which you run the service.js file (bin in our case) where we can find an error file.

{% highlight javascript %}

    at ChildProcess.<anonymous> (C:\Users\username\Documents\projects\PDF_Reports\node_modules\html-pdf\lib\pdf.js:121:17)
    at emitTwo (events.js:106:13)
    at ChildProcess.emit (events.js:191:7)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:215:12)
Error: SetProcessDpiAwareness failed: "COM error 0x80070005  (Unknown error 0x0ffffffff80070005)"

{% endhighlight %} 

But what does the above tells us? Apart that the error happens in html-pdf module (a handlebars-pdf dependancy) not much. Luckily I've found this gem! 
https://stackoverflow.com/questions/37856247/html-pdf-not-creating-file-on-iis-server-with-node-js - It says that 2.0.1 fails but 1.5.0 is working fine! Let's try that!

We run:

{% highlight shell %}
npm install html-pdf@1.5.0 --save
{% endhighlight %} 

Restart the service and success! We have a Windows service which we can start, stop, restart, write a batch file to manage so and our Dev-Ops can manage it and let us work using JS we love! 

I didn't have too much time but this is how you'd run a stored proc using mssql module to pull data out of a SQL Server:

{% highlight javascript %}

const config = {
    user: '...',
    password: '...',
    server: 'localhost', // You can use 'localhost\\instance' to connect to named instance 
    database: '...',
 
    options: {
        encrypt: true // Use this if you're on Windows Azure 
    }
}

  sql.connect(config).then(pool => {	
      // Call stored procedure 
	  return pool.request()
	  .input('AssetId', parameter1)
	  .input('Tag', parameter2)	                     
	  .execute('GetData') // -> Name of the stored procedure
    /*
    * To add another Stored Procedure create a .then() pass the result from previous, add parameters using .input() and call stored proc using execute()
    */
    .then(result => {
	  let document = {
		  template: '<h1>{{msg}}</h1>'+
		  '<p style="color:red">Red text</p>'+
		  '<img src="https://archive.org/services/img/image" />',
		  context: {
			  msg: result
		  },
		  path: "./pdf/report-"+ result +".pdf"
	  }
	   
	  pdf.create(document)
		.then(res => {
			console.log(res)
		})
		.catch(error => {
			console.error(error)
		})
    })
    .then(() => {
      //Close connection pool
      pool.close()
    })
  }).catch(err => {
	  res.send(err)
  })
  
  sql.on('error', err => {
      res.send(err)
  })

{% endhighlight %}

And that's all!
