---
layout: post
title: "Backbone.js for Absolute Beginners - Getting started (Part 1: Intro)"
date: 2012-09-11 22:50
comments: true
categories: [backbonejs, javascript, web frameworks, web development, agile frameworks, tutorials]
---

Backbone.js is a JavaScript framework, among many others, that is gaining special attention in the web development community because it's ease of use and the structure that it provides to JavaScript applications.

(Updated: 2013-02-02, 2013-11-24)

### Brief Background (optional reading)

<a href="#start">TL; DR</a>: You need to use JavaScript heavily in order to make responsive and interactive web applications. <a href="#start">Jump to this and get started.</a>

The web application development process has been evolving over the years. In its beginning… the they were just static HTML pages, which required programmers change the code (HTML, CSS, JS) to change the content. Later, in web 2.0, server side programming languages (like PHP, Ruby, Java, …) were added to generate HTML pages dynamically based on user inputs and data stored in database. That was huge improvement, and most of the pages served today use this approach. However, to provide even more responsiveness of the website, speed and enhance the user interaction, it requiress to bring the logic closer to the client (browser).  There are a couple of languages that can run in the browsers besides JS, such as Java, Flash and others. However, these ones require extra plugins and are not universally accepted as JavaScript.

Therefore, web apps nowadays require heavy use of JavaScript to generate content on the fly and quickly. The user can’t wait between request. A lot of the logic/code that used to be in the server side is being moved to the client side. JS allows the web sites to render only the parts of the website that changed and not the full-page on every request. Examples of this kind of web apps are Gmail, Pandora, Pinterest, Nokia Maps 3D and others.

A common problem with large JS web apps developed is that it became pretty messy really quick. The lacks of structure it’s hard to maintain. This is where Backbone comes into play. It provides structure to organize the code and increase maintainability. Backbone is not the only one; in fact, there are many JS frameworks that accomplish similar results like Ember.js, Angular.js and so on. However, I choose Backbone because is one of the most widely spread framework in its category. It has a vibrant community and it’s also being fully used in production for a considerable number of big companies like: Wal-Mart mobile, Groupon, Khan Academy, Pandora, Wordpress, Foursquare, and so on.

<a id="start"></a>

## Just enough to get started with Backbone.js

Backbone.js has hard dependency on underscore.js and a soft dependency on jQuery. It’s composed by the following modules:

   * Views
   * Events
   * Models
   * Collections
   * Routers

## Shut up and show me the code!
 
Alright! the way we are going to explore all of these modules it’s through examples. This is a practical tutorial that I wished I had it when I stared learning. So, this is a fat-free walkthrough Backbone.js, as simple as it could be, all the code is in one file just for didactical purposes (no hidden magic tricks, all cards are on the board).

The first example is a ‘Hello World’ app in Backbone and the second it’s a Todo App. After doing these 2 apps, you’ll see in action every Backbone module and have practical understanding about them.


## 1. Hello World in Backbone.js

You can follow alone this tutorial's code in this [repository](https://github.com/amejiarosario/Backbone-tutorial/commits/). Each feature implemented it’s a new commit, so you can easily see what changed in every step.

**1.1.- Simple HTML5 and Backbone boilerplate**

To get started download [this simple html file](https://raw.github.com/amejiarosario/Backbone-tutorial/439ff34409dfc01adca7f9f96efcd726295f1aac/backbone-tutorial.html). This file  contains the libraries that you'll need (jQuery, Underscore.js, Backbone.js and Backbone-localStorage.js) and the placeholders for your HTML and JS code. Don't worry about the libraries we are going to explain them, as we need them.

After downloading the afored mentioned file, notice the HTML where all your page will be built using Backbone.Views!

All your js app will be loaded here:

`<div id="container">Loading...</div>`


<a id="1.2"></a>
**1.2.- Backbone's Views**

Backbone's Views are the equivalent of ‘controllers’ on MVC frameworks (like Ruby on Rails), if you are not familiar with MVC frameworks nevermind. Backbone's Views glues together user events (clicks, pressed keys …), render HTML views and templates, and interacts with models which contains the data of the application.

Here is an example of a Backbone.view: READ the code and COMMENTS, then insert this code in the javascript block in the HTML file that you downloaded.

{% codeblock Simple Backbone.View lang:js https://raw.github.com/amejiarosario/Backbone-tutorial/0bf69185f4463a75cb2d5553f8d1ea197323ccff/backbone-tutorial.html Full Code %}
    var AppView = Backbone.View.extend({
      // el - stands for element. Every view has a element associate in with HTML 
      //      content will be rendered.
      el: '#container',
      // It's the first function called when this view it's instantiated.
      initialize: function(){
        this.render();
      },
      // $el - it's a cached jQuery object (el), in which you can use jQuery functions 
      //       to push content. Like the Hello World in this case.
      render: function(){
        this.$el.html("Hello World");
      }
    });
{% endcodeblock %}

**1.3.- Test the app**

After copying the code, open the file, refresh the browser and you should see the 'Hello World' message… right? Wait, if you just seeing just 'Loading…' it's because you need to initialize the view first.

`var appView = new AppView();`

Yay! you have your Hello Wold in Backbone and intro to the View module. (Full code it's [here](https://raw.github.com/amejiarosario/Backbone-tutorial/0bf69185f4463a75cb2d5553f8d1ea197323ccff/backbone-tutorial.html))

**1.4.- Backbone's Templates**

Backbones has a utility/helper library called [underscore.js](http://underscorejs.org/?utm_source=adrianmejia.com) and you can use their template solution out-of-the-box, but you can use any other template solution that you want like [mustache](https://github.com/janl/mustache.js) or [handlerbars](https://github.com/wycats/handlebars.js). Let's stick with _.js's template for simplicity sake.

Underscore.js template has the following signature:

`_.template(templateString, [data], [settings])` 

where in the `templateString` you use the place holder `<%= %>` and `<%- %>` to substitute them with data. The later does HTML escape while the first one doesn't. Moreover, you can use `<% %>` to run any javascript code. 

Let’s see it in action and rewrite our Hello World using template instead.

{% codeblock Simple Backbone.View and Templates lang:js https://raw.github.com/amejiarosario/Backbone-tutorial/c5b131278ecde92f33882c9a2c22ee4119e57d77/backbone-tutorial.html Full Code %}
    var AppView = Backbone.View.extend({
      el: $('#container'),
      // template which has the placeholder 'who' to be substitute later 
      template: _.template("<h3>Hello <%= who %><h3>"),
      initialize: function(){
        this.render();
      },
      render: function(){
        // render the function using substituting the varible 'who' for 'world!'. 
        this.$el.html(this.template({who: 'world!'}));
        //***Try putting your name instead of world.
      }
    });

    var appView = new AppView();
{% endcodeblock %}

Run the app again and verify that it's working with the template.

### Continue with the [2nd part](/blog/2012/09/13/backbone-js-for-absolute-beginners-getting-started-part-2/) and learn more about Backbone's Models, Collections, View and Events!
