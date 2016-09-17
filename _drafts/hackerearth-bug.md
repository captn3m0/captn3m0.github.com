
[Source](https://www.hackerearth.com/notes/how-i-found-a-bug-in-hackerearth/ "Permalink to How I found a bug in HackerEarth")

# How I found a bug in HackerEarth

How I found a bug in HackerEarth

I am not a competitive programmer. I love programming, but more so I love building things. As a result, I rarely participate in coding contests. Even when I do, I try to use languages like Ruby and Python just to see if I can do it _my way_, so to speak.

While trying a contest in Ruby, I realized that I could not use the ruby `prime` library. This is a standard library in Ruby for a long while, and HackerEarth platform runs on 2.1.1, which is quite new.

I reported this as a bug to HackerEarth in September '14. A quick reply from HE made me realize that they weren't understanding the issue:

> Modules like mathn or erb are part of standard library. They are available.
>
> Try using, require 'erb'require 'mathn' in code editor.  
However 3rd party libraries are not available.﻿

I decided to do some tests and check _all standard libraries_ for their availability. For those unfamiliar with Ruby, this is how you load a standard library in ruby:

`require 'prime'`

Using the HackerEarth API, I was able to write some quick code that tested all expected libraries:

    while read lib; do
      SOURCE="require%20'$lib'"
      echo "Testing $lib"
      curl -s -d "client_secret=API_SECRET&lang=RUBY&async=0&source=$SOURCE" http://api.hackerearth.com/code/run/ > $lib.json
    done < libs.txt

Here `libs.txt` contains a list of all standard libraries. The above code is in bash, and makes use of curl. Parsing the results, I replied with the following:

> Requiring the following libraries raises a missing error:
>
> coverage - RE  
extmk - RE  
fiddle - RE  
io/console - RE  
json - RE  
minitest - RE  
minitest/benchmark - RE  
minitest/spec - RE  
mkmf - RE  
objspace - RE  
prime - RE  
psych - RE  
racc - RE  
rake - RE  
rdoc - RE  
rexml - RE  
rinda - RE  
ripper - RE  
rubygems - RE  
tk - RE  
win32ole - RE  
xmlrpc - RE

HackerEarth admitted the issue (I posted code to replicate on [github][1]), and have since worked on it. I just ran the tests again, and only the following libraries are unavailable now:

> curses - RE  
dbm - RE  
debug - RE  
extmk - RE  
gdbm - RE  
generator - RE  
iconv - RE  
racc - RE  
readline - RE  
rexml - RE  
rinda - RE  
tk - RE  
win32ole - RE

A few of these are understandable (`win32` since HE platform runs on Linux, and `tk`, which is a graphical library). A few of these are unavailable in Ruby 2.1.1 (I copied the list of libs from the 2.1.3 docs).

Kudos to HackerEarth for fixing a bug that very few of their users would have faced. All the source code for this post can be found at [github][1].

[1]: https://github.com/captn3m0/ruby-stdlib-test-hackerearth "HackerEarth Ruby stdlib Tests"
  