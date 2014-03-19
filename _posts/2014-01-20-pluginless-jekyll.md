---
layout: post
title: Using Jekyll optimally without plugins
tags: 
 - jekyll 
 - github
 - programming
---

If you're a programmer, by now you've surely heard of the various static-site
compilers that are taking over the world. My pick of choice is Jekyll, (about
which I've [blogged earlier](/blog/2011/09/19/jekyll/) as well) mostly because
it is the default supported tool for the GitHub Pages service. Read [my earlier
blog post](/blog/2011/09/19/jekyll/) if you don't know about Static Site Generators.

Using Jekyll means that it is far more easier for me to host my blog on GitHub
Pages by just writing down posts in plain markdown. Markdown, for those of you
don't know is a simple markup language that uses an email-like syntax that is
then compiled to HTML. 

A lot of power in Jekyll comes from its various plugins, but I've always been
vary of using them as the default host for Jekyll (GitHub Pages) disables
all plugins and runs in safe mode. Plugins are an awesome tool to have, but they
are only good if you are hosting the site on your own machines. I'm not shying
away from using them but want to point out that plain-Jekyll itself is powerful
enough to do most of the tasks. What follows are some examples of how to use
Jekyll optimally.

##Data Files
This is a [recent addition][data-files] in Jekyll that allows you to use
data noted down in YAML format inside the `_data` directory that is accessible
to you anywhere using the `site.data` prefix. For instance, I recently shifted
the [SDSLabs Team Page][team] from plain HTML to Jekyll, and I used a data file
to define all the required elements that are shown for every user. The data file
looks something like this (`_data/members.yml`):

{% highlight yaml %}
- name: "Abhay Rana"
  pic: "abhay.jpg"
  links:
    Facebook: "https://facebook.com/capt.n3m0"
    Twitter: "https://twitter.com/capt_n3m0"
- name: "Team SDSLabs"
  pic: "sdslabs.jpg"
  links:
    Facebook: "https://facebook.com/SDSLabs"
    Twitter: "https://twitter.com/sdslabs"
{% endhighlight %}

Then, I iterate over this data using the following syntax:

{% highlight html%}
{%raw%}{% for member in site.data.members %}{%endraw%}
<img src="pics/{%raw%}{{member.pic}}{%endraw%}" alt="{%raw%}{{member.name}}{%endraw%}">
<div class="img-bar">
  <span class="img-title">{%raw%}{{member.name}}{%endraw%}</span>
  <span class="img-icons">
    {%raw%}{% for link in member.links %}{%endraw%}
    <!-- link[0] holds the hash key = facebook/twitter -->
    <a href="{%raw%}{{link[1]}}{%endraw%}"><img src="assets/{%raw%}{{link[0]|downcase}}{%endraw%}.png"></a>
    <!-- link[1] holds the hash value-->
    {%raw%}{% endfor %}{%endraw%}
  </span>
</div>
{%raw%}{% endfor %}{%endraw%}
{% endhighlight %}

Earlier, you could have achieved the same thing by adding this data to your
`_config.yml` file, but the `_data` folder allows you to store data properly
in various files, if needed.

##Liquid Filters
Since Jekyll relies on [Shopify's Liquid][liquid] language for templating
purposes, it has a very large list of supported functions, filters and markup
tools ready for you to use. For instance, while working on the
[SDSLabs Portfolio][portfolio], I used the split and downcase filter to convert
a known list of categories to single word objects that could be used as file
names.

{% highlight html %}
{%raw%}{% for category in site.data.category %}{%endraw%}
  <!-- category is something like "Web Development"-->
  {%raw%}{% assign category_name = category|split: ' '|first|downcase %}{%endraw%}
  <a href="/category/{%raw%}{{category_name}}{%endraw%}.html">{%raw%}{{ category }}{%endraw%}</a>
{%raw%}{% endfor %}{%endraw%}
{% endhighlight %}

The above snippet converts a string like "Web Development" to a smaller string
"web" that can be used by us for filenames much more easily.

You can check out more liquid filters [over here][liquid-filters]. These include
things like `plus`, `times`, `reverse`, and even `md5` (helpful for gravatars).

##Code Highlighting
Markdown is really awesome, but it lacks Synax Highlighting for code. Jekyll
uses [pygments][pygments] to support syntax highlighting for various languages.
To highlight a piece of code, you just use the following syntax:

{% highlight text %}
{% raw %}{% highlight ruby %}{% endraw %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% raw %}{% endhighlight %}{% endraw %}
{% endhighlight %}

And the output will look like this:

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

##Custom Permalinks
Everyone knows about handling the blog posts permalink using the permalinks
setting in `_config.yml`. But did you know that you can provide custom
permalink to any page in your site? For instance, the Jekyll documentation site
uses the following:

    permalink: /docs/config/

in the frontmatter for the file `docs/configuration.md`. The file would have
been published to `docs/configuration.html` by default, but the permalink in the
file forces it to be published to `/docs/config/index.html`. Its a really nice
setting that allows you to customize the post url for any particular post.

##Raw Liquid Tag
In the rare case that you want to use liquid-like syntax somewhere, say you are
using Handlebars (which uses {%raw%}{{{variable}}}{%endraw%} to echo variables).
You can use the following syntax:
	
	{% assign openTag = '{%' %}
	{% raw %}{% raw %}
	Here is some {{mustache}}
	{% endraw %}{{ openTag }} endraw %}{% raw %}
	{% endraw %}

In fact, I've used the raw tags a lot in this blog post to escape all the liquid
portions. You can see the [liquid documentation][ld] for more help. 

Side Note: Writing the endraw tag in liquid is [really, really hard][endraw].

##Embedding HTML/CSS inside markdown
Sometimes, there are some things that just can't be done with markdown. For
instance, if you need to use a custom tag, or need to write some css within the
markdown document for some reason, there is always a way: just embed content
inside `<div>` tags. This is not a Jekyll feature, but an implementation detail
of Markdown itself, but I think its hacky enough to get a mention here.

    Writing **markdown** here
    <div>
      <style>
        body{
          margin-top: 10px;
      }
      </style>
    </div>
    Back to _Markdown_.

Anything inside a `<div>` tag is untouched by Markdown, and is rendered as it is.

[liquid]: http://liquidmarkup.org/ "Liquid Markup Language"
[ld]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
[endraw]: http://blog.slaks.net/2013-06-10/jekyll-endraw-in-code/
[pygments]: http://pygments.org/
[data-files]: http://jekyllrb.com/docs/datafiles/
[team]: http://team.sdslabs.co/
[portfolio]: http://sdslabs.co/
[liquid-filters]: docs.shopify.com/themes/liquid-basics/output
