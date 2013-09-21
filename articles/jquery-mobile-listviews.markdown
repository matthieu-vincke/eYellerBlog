Title: Format jquery mobile listviews
Author: Matthieu Vincke
Date: 9/21/2013 2:30:47 PM 
Categories: jquerymobile,listviews,css,javascript


This first article will show how to format the jquery mobile listviews to make them do more (a lot more!)

##Basics

- **Jquery mobile classic listviews**


- **Test Code**

- **Test Code**

Blabla

	Test code
	Test

- **Test Code**

Blabla

	Test

Yipiiiiiiiiiii

	Test




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

  