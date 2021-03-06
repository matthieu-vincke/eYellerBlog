Title: Format jquery mobile listviews
Author: Matthieu Vincke
Date: 9/29/2013 5:54:33 PM 
Categories: jquerymobile,css,javascript

This first article will show how to customize the jquery mobile listviews.

jQuery mobile listviews are great but you may find them limited. If it is the case, here are some tips that you can use.


## Introduction ##

Before  starting, let me just clarify what I mean by customizing jQuery mobile. For me, customizing  means  modifying the CSS classes and but also the javascript code. Adding a CSS class to enhance the design of some jQuery mobile items is not a customization for me.

<br/>
**For the little story**

In eYeller, we wanted to represent all the messages around the user on a single page and to be able to display the responses by a click on the message. We also needed a contextual menu to choose to answer to the yell / reyell / get the details => we needed a button inside the header.

As we choose to use jQuery mobile since the beginning, we started to look at the possibilities given by the listviews/collapsibles but it appears that it was a bit limited and it needed some customization. We finally ended up with this result that is not too bad: 
**[Final result after customization](jquery-mobile-listviews/finalResult.htm "Final Result")**


Here is how we did it.

<br/>
**Note**

Please note that I am not a webdesigner and not a CSS expert. I do CSS because I need to and I do it so it can do what I want but I may not be using the best ways to do it. 

If you notice something that can be improved, don't hesitate to let me know so I can make this article better.


##Basics

- **Jquery mobile classic listviews**

If you don't already know the listviews in jquery mobile, have a look at:
**[jQuery mobile listviews demo](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/ "jQuery Mobile Listviews")**

- **What can we do more with listviews?**

jQuery mobile listviews are already great. I like the look and feel of the list-thumb by example: 
**[list-thumb](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-thumb "List-Thumb")**

But, it is not enough if you want to add a lot of information into each entry of the listview. By example, for a yell, you have:
the name, the time, the number of replies, the avatar, the text of the yell, and a button to open the contextual menu. There are also the replies with roughly the same amount of information... 
About the replies... We need to display them after a click on the message. The "collapsible" offers something similar: **[list-collapse](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-collapse "list-collapse")**
But, as you can see, there is no "extended" header for the collapsible: just a single line of text.

I remind you that this is what we want to do: 
**[Final result after customization](jquery-mobile-listviews/finalResult.htm "Final Result")**

You can now see that it is not really possible to do what we want without some customization...


The article will show how to:

- Add a second level: A listview inside another listview (This part is quite easy as we will see it)

- Remove the default icon on the right

- Include some formatted content into the header and into the second level (There is already a way to customize the header but we can do more as we will see: **[list-formatted](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-formatted "Formatted content")**

- Add a button in the listview header and an image at the place I wanted to.

- Extend the "data-filter" feature to make it search into all the listview.

- Move the search bar into a page header

Ready?

<br/>

##Generic listviews
**Create your first listview**

Let's start simple with a simple listview that display the messages.

To help us, I introduce you Towelie and Bender (from SouthPark and Futurama for those who dare not knowing them!)

Here is what they have to say: 

**[Towelie and Bender messages](jquery-mobile-listviews/firstListView.html "Towelie and Bender messages")**

As you can see, it is quite simple and jQuery mobile allow us to do it easily. Just include jquery and jquery mobile js + jquery mobile css and create a listview and that's it!


<jquery-mobile-listviews/firstListView.html>

<br/>
**Second level**

The first level was easy isn't it? But what if someone want to reply to Towelie and Bender? Let say, by example "Cartman" and "Fry"? (I hope you know them? ;) )

They would say something like that: 
**[Responses to Towelie and Bender messages](jquery-mobile-listviews/secondLevel.html "Towelie and Bender messages")**

What do you think? Is it neat enough for you?
Here is how to do that.

To add a second level, you will need first to set the first level as a collapsible in order to make the second level appear after a click on the message.
But, as we saw it in jQuery mobile examples, the collapsible can accept only some text in the header... So, you will need to create some css classes in order to format correctly the data inside the header: a class for the avatar and another for the text and for the avatar in the replies:

    
    .avatar {
	    float: left;
	    margin-top: 1px;
	    margin-left: -10px;
	    margin-right: 5px;	
	    width: 48px;
	    height: 48px;
	    border-radius: 5px;
    }
    
    .listViewHeaderText {
	    white-space:normal;
	    line-height:120%;
	    width:75%;
    }

    .avatarreply {
	    float: left;
	    margin-top: 5px;
	    margin-left: 5px;
	    margin-right: 5px;	
	    width: 48px;
	    height: 48px;
	    border-radius: 5px;
    }  


All the header has to be kept into the "h3" tags. The header becomes:

    <h3> 
	    <p class="avatar"><img src="img/towelieavatar.png"/></p>
	    <p class="listViewHeaderText"><strong>Towelie</strong></p>
	    <p class="listViewHeaderText">Don't forget to bring a towel.</p>  
    </h3>

Then, you can insert the listview in the content part (Same thing, header in the h2 tag...:

      <ul>
        <li>                    
            <h2>
              <p class="avatarreply"><img src="img/Cartmanavatar.png"></p>
              <p class="listViewHeaderText"><strong>Cartman</strong></p>
              <p class="listViewHeaderText">You're the worst character ever, Towelie</p>
            </h2>                    
        </li>
        <li>
            <h2>
              <p class="avatarreply"><img src="img/towelieavatar.png"></p>
              <p class="listViewHeaderText"><strong>Towelie</strong></p>
              <p class="listViewHeaderText">I know...</p>
            </h2>                      
        </li>
      </ul>

To see the result: 
**[Responses to Towelie and Bender messages](jquery-mobile-listviews/secondLevel.html "Towelie and Bender messages")**

If you already know jQuery mobile, you may wandered why we didn't use the collapsible-set instead. That's a good question and the answer is mostly because of the next section: the search bar that is available for the listview and not the collapsible-set unfortunately.... But, as we will see it later, we had to switch to collapsible-set anyway.

<br/>
**Add the search bar**

You want to be able to search into the messages? In real time with no server request? jQuery mobile can help you to do that! Have a look at: **[list-filter](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-filter "list-filter")**

You get it, it is really simple! Just add "data-filter="true"" in the listview, and that's it!

    <ul data-role="listview" data-filter="true">
    

The result is: 
**[Responses to Towelie and Bender messages with search feature](jquery-mobile-listviews/secondLevelWithSearch.html "Towelie and Bender messages and responses with search")**

<br/>
**Add an header**

Adding a header is really easy. Just add a "data-role="header"" in a div on top of the "data-role="content"" and that's it!

Then, you can add some blocks to organize the header in 2 or 3 parts.

By example:

    <div data-role="header" data-position="fixed" data-tap-toggle="false"> 
	    <div class="ui-grid-b">
		    <div class="ui-block-a">
		    	Left part		    
		    </div>
		    <div class="ui-block-b">
		    	Middle part
		    </div>
		    <div class="ui-block-c">
		    	Right part					
		    </div>   
	    </div>
    </div>   

The option "data-tap-toggle" is something you want to remember if you want to avoid some strange behaviour with the forms making the whole page "sliding"... I let you have a look on jQuery mobile to discover this option.

Let's see the result: 
**[SecondLevel with Search and Header](jquery-mobile-listviews/secondLevelSearchHeader.html "Header and search")**

<br/>
**Add a text zone for the date**

There is already a class in jQuery mobile to add some text on the top right corner. It is the CSS "ui-li-aside". 

     <p class="ui-li-aside"><strong>29/09/2013 9:28</strong></p>  

You can use it as it is or customize a bit.
Actually, I like to add this class to it:

    .asideheader{
    	width: 100px;
    	height: 15px;
    	border: solid 1px #CCCCCC;
    	border-radius: 1em 1em 1em 1em;
    	margin-left:-25px;
    	margin-bottom:-5px;
    	text-align:center;
    }  

After this change, it is a bit more funky.
The code becomes for the main message:

    <h3> 
      <p class="avatar"><img src="img/benderavatar.png"/></p>
      <p class="listViewHeaderText"><strong>Bender</strong></p>
      <p class="listViewHeaderText">The chemical energy keeps my fuel charged.</p>  
      <p class="ui-li-aside asideheader"><strong>29/09/2013 9:28</strong></p>              
    </h3>

For the replies, you can use exactly the same syntax.

The result: **[Final Result without custom](jquery-mobile-listviews/finalWithoutCustom.html "Final Result without custom")**

And the final code:

<jquery-mobile-listviews/finalWithoutCustom.html>

<br/>
**Why we need to customize**

Actually, you don't need to if the current result is satisfying for you... But, we wanted for eYeller to:

- Remove the annoying '+' icon
- Put the search bar in the header
- Add a button for a contextual menu

If you do want the same, you also need to customize jQuery mobile. 

<br/>
##Customize it!

**Remove or move the icon**

Removing the icon is quite simple. You just need to create a class "*noicon*" and to make it override "*.ui-collapsible-heading*" and  "*.ui-icon*" and you add this class to the collapsible.

    .noicon .ui-collapsible-heading .ui-icon {		
	    display:none;
    }

And:

    <div id='ListItem'  data-role="collapsible" class="noicon">		

The result is: **[Without the icon](jquery-mobile-listviews/CustomizeStep1a.html "Customize step1a")**


But, if you prefer to move the icon to right and to change it you can something like that:

    .noicon .ui-collapsible-heading .ui-icon {		
	    background: url('img/menu.png') 50% 50% no-repeat!important; 
	    background-size: 18px 18px!important;  
	    left: auto !important;
	    right: 20px !important;	
	    top:38px;
    }  

The result: **[With a new icon](jquery-mobile-listviews/CustomizeStep1a.html "Customize step1a")**

<br/>
**Move the search bar**

The search bar is a nice feature but it takes some space in the main content area. That's why we thought it would be nice to move it into the header.

What we can see also in most mobile app is a button to display or hide the search bar. Let's do that also!

To understand how it works, you have to know that the search bar is simply a "form". So, we can do the trick by overriding the "form" class for our "contentDiv".

But first, we need to modify the header bar as the search bar doesn't fit by default in it.

To do so, we need to modify the CSS class "ui-header".

    .ui-header{
	    background-image: -moz-linear-gradient(top, #3E0470, #111111);
	    background-image: -webkit-linear-gradient(top, #3E0470, #111111);
	    background-image: -o-linear-gradient(top, #3E0470, #111111);  
	    height:50px;
    }

This modification will just add a nice background and set the height to 50px that is the size of the search bar.

Now, second step. As just explained before, we need to modify the "form" class for the "contentDiv" part.

Here is what we can do:

    
    #contentDiv form {
	    background-image: -moz-linear-gradient(top, #3E0470, #111111);
	    background-image: -webkit-linear-gradient(top, #3E0470, #111111);
	    background-image: -o-linear-gradient(top, #3E0470, #111111);
	    
	    position : fixed;
	    top  : 17px;
	    left : 100px;
	    width: 50%;
	    height: 45px;
	    z-index  : 1001; 
    }​

You see the idea? With position fixed, we allow the bar to move and with top/left we set the position. "z-index" is to make sure that the bar is always on top. And finally, the background-image is just for fun! To put some nice background in order to not be differentiate from the header.

See the result here:
**[Move the search bar in the header](jquery-mobile-listviews/CustomizeStep2.html "Move the search bar in the header")**

<br/>
**Toggle the search bar display**

As you may have noticed, the search bar in the header hides the content of the header... it's logical! But, we can add a button in the header to display/hide the search bar and we can make it hidden by default. Let's see how we can do that!

First of all, let's create the button in the header, on the right. 
We can insert a button in the right block of the header simply with:

    <div class="ui-block-c" >
      <div class="insideHeaderMenu">
        <button data-iconpos="notext" id="toggle_btn" onclick="toggle();" data-role="button" data-transition="none"  data-inline="true"  data-icon="mysearch">S</button>
      </div>				
    </div> 

As you can see, the function "toggle" will be called if the user clicks on this button. 
The function needs obviously to display or hide the search bar.
The javascript to do that is:

    function toggle(){
        $("form").toggle();
    }

Easy no? If you have multiple forms in your page, I let you set the correct DOM to target only the search bar.

Finally, if you want to hide it by default, you can add in a "pagebeforeshow" callback:

    $(document).on('pagebeforeshow', '#yells', function(){    
      toggle();    
    });		 

See the result here:
**[Toggle the search bar](jquery-mobile-listviews/CustomizeStep2.html "Toggle the search bar")**

<br/>

**Add a button in yell and replies**

We already know how to add a part on the top right corner with the class "ui-li-aside". All we need is to add some properties to this class to display a button a bit below. The following class does that:

    .insideMenu {
	    float: right;
	    margin-top: 21px;
	    margin-right: 0px;
	    width: 30px !important;
	    height: 40px !important;
	    z-index:1001;		
    }  

In the listview header, it gives:

    <p class="ui-li-aside insideMenu">
		<button data-role="button"  id="show-content" data-iconpos="notext" data-icon="mymenu" onclick="alertTest()">
		</button>	
    </p>	


See the result here:
**[Button in the header](jquery-mobile-listviews/CustomizeStep4.html "Toggle the search bar")**

<br/>

**Some adjustments**

As you may have noticed it, the design is still not perfect, we need some adjustments. 
By example:
- The date of the replies is truncated
- There is no icon for the contextual menu button
- Etc...


After some adjustment, you end up with:
**[Final result](jquery-mobile-listviews/finalResult.htm "Final result")**
Here is the complete code:

<jquery-mobile-listviews/finalResult.htm>


<br/><br/>

## Conclusion ##

As you can see, we can do some great things with the listviews of jQuery mobile. But, you have to know that the performance of the listview is not very good... If you have loads of items in it, it may become slow when you scroll down or up, especially if you have a side menu.

One of the option is to switch to a two levels collapsible instead of a listview with a collapsible on the second level. But, you will lose the search bar functionality as this option is available only for the listviews... I guess life is a choice and so is coding with jQuery mobile!