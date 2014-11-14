---
layout: post
title: "So many forms, which do i use?!?"
date: 2014-10-30 23:06:15 -0400
comments: true
categories: 
---

### About

After being bombarded by forms today I felt a little overwhelmed. While I undertood how to use the different types of forms I was not grasping the overall concept of when I should or could use them. So I sat down to reflect on all this information to come up with as simple a thought process as possible to decide what kind of form I could use...

### Findings

Upon thinking about my predicament and doing a little reviewing it dawned on me that the answer was staring at me in the face all along. The simplicity of the answer actually made me feel a little silly that i hadn't noticed this earlier.
So the answer(which is actually the question you should ask yourself when deciding) to how do you decide what form to use is... *"Is there a **model** associated with the form?"* That's it. I'ts that simple. If the form you are creating has a **model** associated with it then you can (and should cause it's magical) use form_for. If not then you use form_tag or even raw html forms if you feel so inclined.


### Example
  This example is from the *'formal-affair-rails-ruby-006'* lab

  So in one portion of the lab we were asked to made a form for a new baby. Now with my simplified thought process, I ask myself if a baby has a model associated with it. In this case the answer is yes so this is what I do.


  {% include_code for.erb %}

  Now in another part of the lab, I am asked to make a form for a new search. (The specs specifically ask for raw html but for arguments sake I am doing other wise) So I ask myself does a search have a model associated with it? Here the answer is no. Thus I revert to using the form_tag convention to create my form as follows.

  {% include_code tag.erb %}

### SUMMARY

So to sum things up, if you're ever confused on what kind of form you can use just ask yourself this simple question... *"Is there a **model** associated with the form?"*