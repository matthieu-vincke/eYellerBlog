Title: Format jquery mobile listviews
Author: Matthieu Vincke
Date: 9/21/2013 2:30:47 PM 
Categories: jquerymobile,css,javascript

# ***Writing in progress*** #


This first article will show how to customize the jquery mobile listviews to make them do more!

*For the little story*:

In eYeller, we wanted to represent all the messages around the user on a single page and to be able to display the responses by a click on the message. We also needed a contextual menu to choose to answer to the yell / reyell / get the details => we needed a button inside the header.

As we choose to use jQuery mobile since the beginning, we started to look at the possibilities given by the listviews/collapsibles but it appears that it was a bit limited and it needed some customization. We finally ended up with this result that is not too bad: [finalResult](jquery-mobile-listviews/finalResult.htm "Final Result")  (we will see that it is not perfect actually...) 

Here is how we did it.

##Basics

- **Jquery mobile classic listviews**

If you don't already know the listviews in jquery mobile, have a look at:
[jQuery mobile listviews demo](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/ "jQuery Mobile Listviews")

- **What can we do more with listviews?**

jQuery mobile listviews are already great. I like the look and feel of the list-thumb by example: 
[list-thumb](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-thumb "List-Thumb")

But, it is not enough if you want to add a lot of information into each entry of the listview. By example, for a yell, you have:
the name, the time, the number of replies, the avatar, the text of the yell, and a button to open the contextual menu. There are also the replies with roughly the same amount of information... 
About the replies... We need to display them after a click on the message. The "collapsible" offers something similar: [list-collapse](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-collapse "list-collapse")
But, as you can see, there is no "extended" header for the collapsible: just a single line of text.

I remind you that this is what we want to do: [finalResult](jquery-mobile-listviews/finalResult.htm "Final Result")

You can now see that it is not really possible to do what we want without some customization...


The article will show how to:

- Add a second level: A listview inside another listview (This part is quite easy as we will see it)

- Remove the default icon on the right

- Include some formatted content into the header and into the second level (There is already a way to customize the header but we can do more as we will see: [list-formatted](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-formatted "Formatted content")

- Add a button in the listview header and an image at the place I wanted to.

- Extend the "data-filter" feature to make it search into all the listview.

- Move the search bar into a page header

Ready?

##Generic listviews
**Create your first listview**

Let's start simple with a simple listview that display the messages.

To help us, I introduce you Towelie and Bender (from SouthPark and Futurama for those who dare not knowing them!)

Here is what they have to say: [Towelie and Bender messages](jquery-mobile-listviews/firstListView.html "Towelie and Bender messages")

As you can see, it is quite simple and jQuery mobile allow us to do it easily. Just include jquery and jquery mobile js + jquery mobile css and create a listview and that's it!


<jquery-mobile-listviews/firstListView.html>


**Second level**

The first level was easy isn't it? But what if someone want to reply to Towelie and Bender? Let say, by example "Cartman" and "Fry"? (I hope you know them? ;) )

They would say something like that: [Responses to Towelie and Bender messages](jquery-mobile-listviews/secondLevel.html "Towelie and Bender messages")

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

Here is the complete code:

<jquery-mobile-listviews/secondLevel.html>

To see the result: [Responses to Towelie and Bender messages](jquery-mobile-listviews/secondLevel.html "Towelie and Bender messages")

If you already know jQuery mobile, you may wandered why we didn't use the collapsible-set instead. That's a good question and the answer is mostly because of the next section: the search bar that is available for the listview and not the collapsible-set unfortunately.... But, as we will see it later, we had to switch to collapsible-set anyway.

**Add the search bar**

You want to be able to search into the messages? In real time with no server request? jQuery mobile can help you to do that! Have a look at: [list-filter](http://jquerymobile.com/demos/1.3.0/docs/widgets/listviews/#list-filter "list-filter")

You get it, it is really simple! Just add "data-filter="true"" in the listview, and that's it!

    <ul data-role="listview" data-filter="true">
    

The result is: [Responses to Towelie and Bender messages with search feature](jquery-mobile-listviews/secondLevelWithSearch.html "Towelie and Bender messages and responses with search")




**Why we need to customize**



##Customize it!

**Remove the icon**


**Move the search bar**


**Add a text zone for the date**


**Add a button in yell and replies**


**Some adjustments**
