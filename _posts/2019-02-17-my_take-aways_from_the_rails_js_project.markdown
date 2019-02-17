---
layout: post
title:      "My take-aways from the Rails and JS project"
date:       2019-02-17 12:24:30 -0500
permalink:  my_take-aways_from_the_rails_js_project
---


For a start I used my old Rails MVC project that registers Users that can create Campsites and list their own Favorites. The idea was to dynamically change the DOM using JS and jQuery. So during the process I came accross a few "issues" that I had to solve:

**1. I wanted to attach an event handler to a dynamically created DOM element that did not yet exist :-)**

And yes, it is possible! Here is what I read in the jQuery documentation:

> jQuery .on()direct and delegate
> .on( events [, selector ] [, data ], handler )
> The .on() method attaches event handlers to the currently selected set of elements in the jQuery object.
> If selector is omitted or is null, the event handler is referred to as direct or directly-bound.
> When a selector is provided, the event handler is referred to as delegated.
>** Delegated event handlers have the advantage that they can process events from descendant elements that are added to the document at a later time. **

In my case I used delegate event handler when rendering the list of Campsites and I attached click events to an `<h>` tag and a `<button>` that were created after the `listenForCamps()` handler was triggered. Here is what my code looks like:

```
function listenForCamps () { 
    $('#camps').on('click', function() {
        clearData();
        listCamps();
    })

    // event delegation, so that an event handler can be attached to the newly created element
    $('div').on('click', '.item', function(e){
        clearData();
        console.log(e.target.id);
        showCamp(e.target.id);
    });

    // the button only exists after camp list loads
    $('div').on('click', 'button.favorite', createFovorite);
}
```
Notice that when using a delegate event, you specify the parent element  first `$('div')`and then inside the `on()` function the child selector `'.item'` is provided.
Problem solved!

**2. Understanding the project requirement "The Model Objects must have at least one method on the prototype"**

I will try to explain what my "googling" made clear for me. So first of all we have to remember that there are static(class) methods and instance methods, and the difference is clear - the static method works on the `Class`, while the instance method works on the `instance of the Class`. Second we have to be aware thet there is ES5 and ES6 syntax. Consider the examples below:

**ES5**
```
//defining a Class
function Campsite(name) {
  this.name = name;
}

//static method, it is invoked on the class, not on an instance
Campsite.formHTML = function() {
 return (`<form id='new-camp-form'>
                <div>
                    <input type="text" placeholder="name">
                </div>
                <div>
                    <button class="button">Submit</button>
                </div>
            </form>`)
};

//an instance method, it is invoked on an instance of the class
Campsite.prototype.html = function() {
 return(`<div>
        <h4>${this.name}</h4>
    </div>`)
}
```

**ES6**
```
class Campsite {
  constrictor(name){
  this.name = name;
  }

// this is the static(class) method
 static formHTML () {
    return (`<form id='new-camp-form'>
                <div>
                    <input type="text" placeholder="name">
                </div>
                <div>
                    <button class="button">Submit</button>
                </div>
            </form>`)
  };

// this is the instance method
html() {
  return(`<div>
          <h4>${this.name}</h4>
      </div>`)
  }
}

```
All clear?!
So was I asked to create an instance method, and why on the prototype?!
Now where does the confusion come from - many developers prefer declaring instance methods on the PROTOTYPE (i.e. `Campsite.prototype.html`), rather than in the class definition, even if they are using ES6.
The reason is **performace!** Doing so, you will have only one instance of `html() `method in memory and all `Campsite` instances will share it, vs multiple instances of the same `html()` will be created if the method is declared within the class definition.
Now it's clear!

**3. Fetch vs XMLHttpRequest**
Here is what documentation says:
> "The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. It also provides a global fetch() method that provides an easy, logical way to fetch resources asynchronously across the network."
 >

In case you want to dive in, read morea about it [here](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch).
For me it wasn't so much about figuring out what the positives of `fetch` were, it was more like "it is the right way to do it", it just felt more natural, easy to write an fun :)
<iframe src="https://giphy.com/embed/3o6Zt8CQmqiIp0aN6U" width="480" height="338" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/southparkgifs-3o6Zt8CQmqiIp0aN6U">via GIPHY</a></p>


