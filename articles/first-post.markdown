Title: eYeller Blog powered Git blog using Wheat
Author: Matthieu Vincke
Date: Sat Aug 24 2013 09:23:00 GMT+0100
Categories: node,blog,wheat,eYeller

##Introduction

This blog has been created thanks to the <a href="https://github.com/creationix/wheat/" target="_blank">Wheat engine</a> created by [Tim Caswell](https://twitter.com/creationix).

And also thanks to the instructions given in the article:
<a href="http://blog.davydewaele.be/" target="_blank">A node powered Git Blog using Wheat</a> written by [Davy De Waele](https://twitter.com/ddewaele).

##Some tests

- **Test Image**

![Development mode](http://www.gravatar.com/avatar/aa9d29ca4e5f7d3889e715f56bcf6c7d.png)

- **Test Code**

In order for our Wheat powered blog to work, we need to install a couple of required node modules. This can be done manually by executing the commands below in the MyPersonalBlog folder you just created :

	npm install wheat
	npm install stack
	npm install creationix

- **Last Test**

  Our **content repository** also needs 3 other important folders so we need to create those as well :

 - articles
 - authors
 - skins
 
The content of the server.js looks like this (Feel free to change the listen port, currently set at port 80):

	// Just a basic server setup for this site
	var Stack = require('stack'),
	    Creationix = require('creationix'),
	    Http = require('http');

	Http.createServer(Stack(
	  Creationix.log(),
	  require('wheat')(__dirname +"/..")
	)).listen(80);

  