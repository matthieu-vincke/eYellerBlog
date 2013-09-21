Title: Format jquery mobile listviews
Author: Matthieu Vincke
Date: 9/21/2013 2:30:47 PM 
Categories: jquerymobile,listviews,css,javascript

# ***Writing in progress*** #


This first article will show how to customize the jquery mobile listviews to make them do more (a lot more!)

##Basics

- **Jquery mobile classic listviews**

If you don't already know the listviews in jquery mobile, have a look at:
[jQuery mobile listviews demo](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/ "jQuery Mobile Listviews")

- **What can we do more with listviews?**

jQuery mobile listviews are already great. I like the look and feel of the list-thumb by example: 
[list-thumb](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-thumb "List-Thumb")

But, it is not enough if you want to add a lot of information into each entry of the listview. By example, for a yell, you have:
the name, the time, the number of replies, the avatar, the text of the yell, and a button to open the contextual menu. There are also the replies with roughly the same amount of information... 

It is not really possible to do that without some customization...


The article will show how to:

- Add a second level: A listview inside another listview (This part is quite easy as we will see it)

- Remove the default icon on the right

- Include some formatted content into the header and into the second level (There is already a way to customize the header but we can do more as we will see: [list-formatted](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-formatted "Formatted content")

- Add a button in the listview header and an image at the place I wanted to.

- Extend the "data-filter" feature to make it search into all the listview.

- Move the search bar into a page header?

##Generic listviews
**Create your first listview**

<jquery-mobile-listviews/firstListView.html>


**Second level**

**Add the search bar**

##Customize it!

**Remove the icon**


**Move the search bar**


**Add a text zone for the date**


**Add a button in yell and replies**


**Some adjustments**


##Some tests


<jquery-mobile-listviews/test.js>


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

  