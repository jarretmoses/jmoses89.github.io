---
layout: post
title: "event.stopPropagation(); <--semicolon remembered"
date: 2014-11-13 23:36:18 -0500
comments: true
categories: 
---
###Preface

Yesterday during lecture, wea glossed over the concept of event.stopPropagation(); What is it? That's a good question. Mainly, I wanted to udnerstand what the concept of 'bubbling up the DOM tree' meant. I decided to sit down and play around with some javascript to find out.

#### Test Subjects
{% img /images/div.png %}

#### Hacking Around

#####Code 1
```javascript
$(function(){
  $('.div1').click(function(){
    alert("Hey I'm Steven!");
  });
});
```

In my first start to ficure out what event.stopPropagation() is I placed a div inside a div and added an event handler to the outer div which would display an alert anywhere I clicked inside div1..including div2. So since div2 is inside div1 div2 counts as part of div1. That makes sense but doesn't yet solve my problem.

#####Code 2
``` javascript
    $(function(){
      $('.div1').click(function(){
        alert("Hey I'm Steven!");
      });
      $('.div2').click(function(){
        alert("Hey I'm Tristan!");
      });
    });
```
 Here is where thhings get interesting. If I click outside of Tristan, only Steven's alert will pop up. However, If I click inside of Tristan(red) I will have an alert box pop up saying 'Hey I'm Tristan!', but then following that I get an alert saying 'Hey I'm Steven!' Here I start to udenrstand the concept of bubbling. Since Tristan is inside of Steven, even though there is an event handler inside Tristan, Steven will still be triggered.


 #####Code 3
``` javascript
    $(function(){
      $('.div1').click(function(){
        event.stopPropagation();
        alert("Hey I'm Steven!");
      })
      $('.div2').click(function(event){
        event.stopPropagation();
        alert("Hey I'm Tristan!");
      })
    });
```
This is where it all makes sense. While clicking on Steven still works the same, when I click on Tristan, I only get the alert associated with this event handler. 


####Summary

After playing around with this concept I have come to understand that stopping propagation relates to when sibling elements and their parents both have event watchers. Without event.stopPropagation(): the child and any of its parent's events will be triggered. However with it, the event will be isolated, thus stopping the 'bubbling' up the DOM.

{% img /images/dance.gif %}
