---
layout: post
title:      "Data here, data there, data everywhere"
date:       2018-01-09 18:30:03 +0000
permalink:  data_here_data_there_data_everywhere
---


Hashes was fun, reading about nested hashes was "Yeah, that is clear!"
But then, when you start manipulating nested hashes - oh, my God!
What happened, why is it returning nil, when I expect a string?
After a few hours struggling with nested hashes, a good night's sleep and a few hours more, I came up with this idea:

**Nested hashes are like labled boxes put in one another!**

Inside some box there could be two, three or more smaller labelled boxes.
Iterating on nested hashes became easier when you think of them as boxes - you just have to keep track which box have you just opened ( label.each do | | ) and how many boxes you can see in it.

Hope this helps you, too!
