---
layout: post
title: Programming in Node.JS
tags:
- learning
- nodejs
---

After my attempts at [python](http://captnemo.in/blog/2011/05/16/learning-python), [Ruby on Rails](https://rubyonrails.org), this was the time for node.js. You ask me what is node.js ? Remember when Google Chrome came out and went [blazing past the rest of the browsers](http://stackoverflow.com/questions/40994/is-google-chromes-v8-engine-really-that-good) in Javascript benchmarks. That was because of its internal Javascript Engine, called [V8](http://code.google.com/p/v8/).

Soon, V8 was developed as a backend to an evented IO library, that is now known as [node.js](http://nodejs.org). Initially, it was named just node, but to prevent confusion, and explain its javascript inheritance, it was renamed node.js. This is the water-cooler moment of the language. If you know node, you're the cool guy on the block. So what is so special in node ?

## Evented IO

Basically node allows you bring home the same good anonymous functions from [JQuery](http://jquery.org) on your server. In advanced terms, node allows evented input/output, meaning all the IO calls are non-blocking and evented, or scheduled in parallel.

### Traditional I/O:
<pre class="prettyprint">
data = file.read("/foo/bar");
  // wait...
  doSomething(data);
</pre>

### Evented I/O:
<pre class="prettyprint">
file.read("/foo/bar", function(data) {
  // called after data is read
  doSomething(data);
});
otherThing(); // execute immediately;
</pre>

## How To Install

The official installation guide is present at <https://github.com/joyent/node/wiki/Installation>. I'd present a slightly different version, using `nvm`, i.e [Node Version Manager](https://github.com/creationix/nvm).

### Unix/Linux

#### Dependencies
There are some dependencies on installing node.

`sudo apt-get install git-core build-essentials libssl-dev`

Run the corresponding command for your distro (yum etc).

#### Installing nvm

1. Clone nvm:
`git clone https://github.com/creationix/nvm.git ~/.nvm`
2. Include nvm:
`. ~/.nvm/nvm.sh` //The dot is important
3. Source it to your bash file. Basically copy the above command(2) inside your ~/.bashrc.

#### Fetching node
Node is under heavy development at the moment. Development of node is carried across a stable & a testing branch. The stable branch is the one that you should prefer. As of now, `stable` is `v0.4.11` and testing has reached `v0.5.6`.

Now run the following commands:
`nvm install v0.4.11` to install v0.4.11
`nvm use v0.4.11`
`nvm alias default v.04.11` to make it default

You can type `which node` to see the actual node binaries being used.

#### Package Methods
I would strongly advice against using your distro versions of node, unless you are on a rolling release distro, such as Arch. Please do not run `sudo apt-get install node` to install node. This would only cause much anguish and pain later on.

As of now, even the beta of Ubuntu 11.10 holds `v0.4.9` and is likely to do so for the next 6 months.

### Windows
As I've stopped using Windows for quite some time, here are instructions from the official node installation guide.

**Windows Build (Node v0.5.5)**: <http://nodejs.org/dist/v0.5.5/node.exe>
I would again recommend to install <http://nodejs.org/dist/v0.4.11/node.exe> for stability reasons.

Self-contained binaries are available at <http://node-js.prcn.co.cc>

### Node Package Manager
All cool programming languages come with their own package managers. Ruby has [rubygems](https://rubygems.org), Python has pip, PHP has PECL, perl has CPAN, and `node` has [npm](https://github.com/isaacs/npm).

`npm` holds a large collection of packages that are the extra batteries that don't come included in node. If you need to parse documents, or do some other fancy stuff in node, don't look farther than npm. If you need it, chances are, it already has a package in npm. See [list of packages](https://www.npmjs.com/) on the npm site.

#### Unix

A simple one line install is available for `npm`

`curl http://npmjs.org/install.sh | sh`

After that, you can install any package by `npm install package`. For instance, install jade by `npm install jade`

Windows folks can clone the [npm repository](https://github.com/isaacs/npm) and run the included `nmp.bat` file, and hope that it works.

## Simple Servers in Node

node.js comes with "batteries included", and part of that battery is node's ability to instantly create web servers. Yes, right inside your program, you can easily create web servers, which will hold full compliance to HTTP.

This is a very simple HTTP server, written using the http module(included) in node :

<pre class="prettyprint">var http=require('http');
http.createServer(function(request, response) {
  var headers = { "Content-Type": "text/plain" };
  response.sendHeader(200, headers);
  response.sendBody("Hello, World!\n");
  response.finish();
}).listen(8000);
</pre>
As you can see, the createServer function takes a callback function as its argument. The callback function is called for each of the requests. All events are handled easily and instead of a server handling threads, memory etc, node just handles requests. In essence, a request generates an *event*, which is then handled by the callback function provided.

This is quite similar to the way we program event loops in javascript on the browser.

## The good stuff
There are loads of interesting projects using node. Visit the [modules section](https://github.com/joyent/node/wiki/modules) on the node wiki for a list of interesting node modules available. These include node clients for various libraries such as [Databases](https://github.com/joyent/node/wiki/modules#wiki-database)(mysql, postgre, sqlite, Cassandra etc), Microframeworks (lik Sinatra), Frameworks, wikis, CMS, parsers and what not.

I'd recommend starting out with [Connect](https://github.com/senchalabs/Connect) which is a middleware for node, and allows you to wrap your application easily around it. For databases, you can either go with the standard Relational ones(like mysql) or be brave, and take a spin with the noSQL ones like CouchDB, Cassandra, or MongoDB. All of them have native bindings available for node.js.

## References
* [Node On GitHub](https://github.com/joyent/node/), including the wiki, documentation & code
* [Nodejs.org](http://nodejs.org/)

## Blogs & Other resources
* [NodeJitsu](http://blog.nodejitsu.com/), a company working completely on node. ![][dead]
* [Getting Started with Node.JS, Express and CouchDB](http://www.bytemuse.com/2011/06/getting-started-with-node-js-express-and-couchdb/)
* [6 Must Have Node.js Modules](http://blog.nodejitsu.com/6-must-have-nodejs-modules)
* [Some cool node projects](http://addyosmani.com/blog/spotlight-issue1/)
* [HowToNode](http://howtonode.org/)
* [The node Beginner book](http://nodebeginner.org/)
* [NodeCasts](http://nodecasts.org/)

## [StackOverflow](http://stackoverflow.com) Questions on node
* [How to store Node.js deployment settings/configuration files?](http://stackoverflow.com/questions/5869216)
* [How do I get started with NodeJS](http://stackoverflow.com/questions/2353818/how-do-i-get-started-with-nodejs)
* [What is node.js](http://stackoverflow.com/questions/1884724/what-is-node-js)
* [Where to host node.js applications](http://stackoverflow.com/questions/3648993/where-can-i-host-a-node-js-app)

[dead]: https://img.shields.io/badge/status-dead-red.svg?style=flat-square