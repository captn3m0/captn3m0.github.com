---
layout: post
title: What was the first project on GitHub?
---
**Note**: This is cross-posted from [Quora](https://qr.ae/CW76f) where I wrote this answer initially.

The first project on GitHub was **grit**. How do I know this? Just some clever use of the search and API.

[Here's a GitHub search](https://github.com/search?q=created%3A%3C2008-01-15&amp;type=Repositories&amp;ref=searchresults) to see the first 10 projects that were created on GitHub. The search uses the `created` keyword, and searches for projects created before 15 Jan 2008.

They are (in order of creation) (numeric id of repo in brackets):

1.  [mojombo/grit](https://github.com/mojombo/grit) (1)
> Grit gives you object oriented read/write access to Git repositories via Ruby.
> Deprecated in favor of libgit2/rugged
2.  [wycats/merb-core](https://github.com/wycats/merb-core) (26)
> Merb Core: All you need. None you don't.
> Merb was an early ruby framework that was merged to Rails
> No longer maintained.
3.  [rubinius/rubinius](https://github.com/rubinius/rubinius) (27)
> Rubinius, the Ruby Environment
> Still under active development
4.  [mojombo/god](https://github.com/mojombo/god) (28)
> God is an easy to configure, easy to extend monitoring framework written in Ruby.
> Still actively maintained, and use by GitHub internally as well, I think
5.  [vanpelt/jsawesome](https://github.com/vanpelt/jsawesome)(29)
> JSAwesome provides a powerful JSON based DSL for creating interactive forms.
> Its last update was in 2008
6.  [wycats/jspec](https://github.com/wycats/jspec) (31)
> A JavaScript BDD Testing Library
> No longer maintained
7.  [defunkt/exception_logger](https://github.com/defunkt/exception_logger) (35)
> The Exception Logger logs your Rails exceptions in the database and provides a funky web interface to manage them.
> No longer maintained>
8.  [defunkt/ambition](https://github.com/defunkt/ambition) (36)
9.  [technoweenie/restful-authentication](https://github.com/technoweenie/restful-authentication) (42)
> Generates common user authentication code for Rails/Merb, with a full test/unit and rspec suite and optional Acts as State Machine support built-in.Maintained till Aug 2011
10.  [technoweenie/attachment_fu](https://github.com/technoweenie/attachment_fu) (43)
> Treat an ActiveRecord model as a file attachment, storing its patch, size, content type, etc.

I'm sure the id from 2-25 would be taken up by many of the internal GitHub projects, such as github/github. To get the numeric id of a repo, visit [https://api.github.com/repos/mojombo/grit](https://api.github.com/repos/mojombo/grit) and change the URL accordingly.