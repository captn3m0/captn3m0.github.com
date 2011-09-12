---
title: Learning Ruby on Rails
layout: post
---
Continuing my quest on Web Designing, I've started learning [Ruby On Rails][ror], which is like *the* most-hyped web framefork of the moment. After all, [Github][gh] runs on Ruby On Rails, [Redmine][red] uses Rails, and so do [Basecamp](http://basecamphq.com),[Hulu](http://hulu.com),[Scribd](http://scribd.com), and even [Twitter](http://twitter.com). Even though RoR has Ruby in its name, its just a namesake. 

Learning Ruby and learning Rails are entirely two different routes, and learning one only gives you a slight advantage in the other. I'm learning Rails by the excellent book, [Ruby On Rails 3 Tutorial][ror3t], by Michael Hartl. It covers Rails 3, which is one reason I picked it as Rails 3 is quite different from Rails 2 in comparision.

Rails in a few words would be described as *a Web framework that makes writing web applications really, really easy*. And I really mean that. I've been programming in Rails for ~2 days, and I can confortably say that it is better than any other PHP framework (viz [CakePHP](http://cakephp.org), [CodeIgniter](http://codeigniter.com), [Kohana](http://kohanaphp.com)) simple because it is powered by Ruby. 

And the beauty of Ruby is not in its implementation, but in its elegance. Reading ruby code is lie reading seeing a visual presentation. While PHP is the paragraphed, prose version of the same stuff. Simply put, PHP allows you to do the same things, but essentialy it was not readable enough to match Ruby's elegance.

Rails follows the [MVC pattern][mvc] (Model-View-Controller) for development, and uses it strictly. It has got its own conventions, but as I found out, the concept of convention over Configuration makes much more sense in Rails than it ever did in PHP. All that time I spent in the CakePHP console was nothing compared to the interactivity of the Rails Console(`rails c`). Starting development server(`rails s`) is as easy as running the production server(`rails s --environment production`).

Instead of writing down *another* beginner tutorial on Rails, I'd rather direct you to some of the excellent Rails resources :

* [Ruby on Rails 3 Tutorial][ror3t], the book I'm reading for learning Rails. Highly recommended
* [RailsBrains](http://railsbrains.org), offline API for Rails
* [Rails Getting Started](http://guides.rubyonrails.org/getting_started.html), Official Rails Getting Started guide
* [Rails@Stackoverflow](http://stackoverflow.com/questions/tagged/ruby-on-rails)

[red]: http://redmine.org "A project management system with code browsing"
[gh]: https://github.com "GitHub"
[ror]: http://rubyonrails.org "Official RoR Site"
[ror3t]: http://ruby.railstutorial.org/ruby-on-rails-tutorial-book "Ruby On Rails 3 Tutorial"
[mvc]: http://en.wikipedia.org/wiki/Model-view-controller "Model View Conroller"
