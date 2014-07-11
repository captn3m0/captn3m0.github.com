---
layout: post
title: Coming back to rails
tags: 
 - rails
 - ruby
 - features
---

I've 
[worked with rails previously before](/blog/2011/08/01/learning-ruby-on-rails/)
, but that was a long time back
and even though I've continued to dabble with it, 
I'd never built anything complete or large enough with it. This time,
however, I'm working on an actual large-scale application with all the 
nuts-and-bolts that make rails such a pleasure to work with. Since
I'm coming back to rails after such a long time, I thought I'd document
some of the cool new features that I've found in rails this time around.

**Spring** - One of the major discomforts of working with rails on the
command line was that it is *heavy* and *slow*. Spring works behind
the scenes on the second issue, namely speed. Here's how the
project's README describes itself:

>Spring is a Rails application preloader. It speeds up development 
by keeping your application running in the background so you don't 
need to boot it every time you run a test, rake task or migration.

You can update all the binaries in your `PROJECT_ROOT/bin/` directory
(which include `rails`, `bundle` and `rake`) to make use of spring
by executing the following command:

    bundle exec spring binstub --all

Any further execs (such as `./bin/rake -T`) will make use of
the spring pre-loader leading to much faster startup times. You can even
use spring against the default system binaries by prefixing the commands
with `spring`, such as `spring rake -T`.

**Resque-Scheduler** - 
I needed a job queue for background tasks and polling API
services, and what better tool to use than resque. I'm using it in combination
with  [resque-scheduler](https://github.com/resque/resque-scheduler) for
running tasks on cron. How it works is that in addition to your main rails
server and a long running resque job process, a separate resque-scheduler
rake task is kept running, which loads up the schedule and inserts
tasks accordingly into the resque queue as per the schedule.

For those new to resque in general, you can start the two processes by:

{% highlight sh %}
QUEUE=* rake environment resque:work #To start resque
rake resque:scheduler
{% endhighlight %}

Note that we are pre-loading the rails environment in the resque:work task as
it will load rails for you across all of your tasks. Also note that you
will need the following two lines in your `Rakefile` to get these tasks to run:

{% highlight ruby %}
require 'resque/tasks'
require 'resque/scheduler/tasks'
{% endhighlight %}

Also remember to define the `resque:setup` task according to the 
`resque-scheduler` README, which would load the schedule and config as needed.

This blog post is a work-in-progress and I will continue to update it with
bits of rails-foo as I learn more.