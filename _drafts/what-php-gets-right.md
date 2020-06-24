---
layout: page
title: What PHP gets right
permalink: /what-php-gets-right/
---

Unlike what the internet may have you believe, PHP gets a lot of things right. Not just right, it gets a lot of stuff _perfect_, especially from a time-starved developer's PoV. It is the perfect language for "getting-shit-done"[^1]. I thought I'd document these, so that other languages don't keep getting this wrong.

I'm framing this primarily against Python, but that is only because Python happens to be the best concrete reference point to use - they are both fairly similar languages used for similar usecases. Once again, the point of this is not for you to come up with counter-examples where Python gets it better, but to help non-PHP developers understand why PHP is as popular as it is. Some of these are tiny differences, some are language-design things that can't be changed, and a lot of it is ecosystem specific - so don't expect much consistency between point to point.

## Documentation

### Structure

The biggest difference is in the approach to PHP and Python's documentation. In PHP, every function _gets its own webpage_. Python has a webpage per module. Let's take a simple method: `floor` for eg. So the Python reference for floor happens to live at `docs.python.org/3/library/math.html#math.floor`, while PHP has its at `php.net/manual/en/function.floor.php`.

This is how the searches for each compares[^2]:

|Python|PHP |
|------|----|
|![](/img/pvp/python/floor.jpg)|![](/img/pvp/php/floor.jpg)|

In case you missed the difference, the link for Python's documentation goes to the top of the page, instead of taking you to the specific `floor` method. Also note that the documentation for various Python versions live in separate links. You can't refer to the same page, even between minor versions (3.7 and 3.8 have different docsites).

### Clarity

This is the entirety of the Python documentation on the floor method:

> `math.floor(x)`
>    Return the floor of x as a float, the largest integer value less than or equal to x.

To get anything beyond the function signature, you have to read and understand the english text. This isn't necessarily bad, this is what most languages tend to do (MDN is another place which gets this right) - convert the docstring comment into a text that you use as documentation.

This is [how the PHP page looks](https://www.php.net/manual/en/function.floor.php):

![](/img/pvp/php/floor-docs.jpg)

In case it isn't obvious to you, this is what all it does better:

1. It is skimmable. ou can skip down to just the return value
2. It tells you the rationale behind the return value being float (so you don't go and typecast it to a integer for eg)
3. Tells you what happens if you pass a non-real input.
3. A short text for each argument it takes.
4. Examples!
5. References to similar methods (ceil and round)
6. It tells you which all versions of PHP has the method
7. Gives you a way to "edit" it. The link goes to `https://edit.php.net/?project=PHP&perm=en/function.floor.php`
8. Gives you a way to report a bug with the documentation. The link goes to `https://bugs.php.net/report.php?bug_type=Documentation+problem&manpage=function.floor`

Python on the other hand:

1. Lets you report a bug, but it takes you to `https://docs.python.org/3/bugs.html`, which doesn't triage the bug for you.
2. `math.floor` raises a Runtime exception if you pass it a list, but anyone reading the docs wouldn't know that - you'd have to understand how types and implicit casting works in Python works.
3. No references, or links.
4. Having a non-living documentation means developers pay a overhead cost of having to ensure that they are on the right page every time.

(4) is a very real problem. Even something as simple as `floor` changes (the previous was Python 2, this is Python 3):


> math.floor(x)
>
>   Return the floor of x, the largest integer less than or equal to x. If x is not a float, delegates to `x.__floor__()`, which should return an `Integral` value.

WTF is Integral, you wonder? Thankfully, it links directly to [the `class numbers.Integral` section](https://docs.python.org/3.7/library/numbers.html#numbers.Integral) which says:


> class numbers.Integral
>
>   Subtypes Rational and adds a conversion to int. Provides defaults for float(), numerator, and denominator. Adds abstract methods for `**` and bit-string operations: `<<, >>, &, ^, |, ~.`

That's all the documentation you get. What this text misses out is in telling you that:

- this is an internal type that you don't need to worry about
- the list of types that use this.

This is exactly the kind of usecase where an example is a thousand times better. Seeing something like:

```python
class Cost:
  """ Returns the cost as the closest hundred """
  def __floor__(self):
    return (self.money / 100) * 100
```

makes it so much easier to understand.

### Examples

PHP has official examples for a lot of functions. As an example, lets take the `base_convert` function. Before I get to the example, here's a partial screenshot which shows off 2 other things that PHP gets right:

![](/img/pvp/php/base-convert.jpg)

1. The **Warning** is in bold, and links to a very relevant page which points out the function's limitations.
2. The changelog is its own section, and tabulated. This makes it much more accessible.

And back to examples:

![](/img/pvp/php/base-convert-example.jpg)

Python on the other hand doesn't have a helper method, and all you get is a [StackOverflow](https://stackoverflow.com/questions/2267362/how-to-convert-an-integer-to-a-string-in-any-base) question with 29 different approaches[^3].

### Changelog

While Python gets warnings okay (they are at a module level, rarely at a method level), the same doesn't quite work for version changes. A simple example is how new hashes are covered in `hashlib`. The documentation for `blake2` lives at `docs.python.org/3/library/hashlib.html#blake2`, and if you read the page from that link to the end, you wouldn't realize that Blake 2 isn't available before Python 3.6. You have to scroll to the top of the page, and make sure you read the finetext:

![](/img/pvp/python/hashlib.jpg)

This is how PHP covers a similar issue, by adding a Changelog in the `password_hash` function:

![](/img/pvp/php/phash.jpg)

## Helper Functions

One of the major reasons for the millions-of-modules problem in the Node ecosystem is the fact that Node doesn't have a standard library that _helps the developer_. As an example, read through the [Node.js documentation for `fs`](https://nodejs.org/api/fs.html) and notice how much of the design is just derivative of unix file APIs. Node does the bare minimum, and so do most other languages - if you have exposed the OS methods, the rest is for developers to build themselves. If building small correct implementations is hard, it either:

1. Gets implemented in a small module that becomes widely used. See the source for [is-integer](https://github.com/parshap/js-is-integer/blob/e9ace1119557f8d942448cd0251b77bb508c6edb/index.js#L4-L8) npm module, which has 200,000 downloads every week.
2. Or your language can helpfully provide it.

PHP takes second opposite approach: it has a `is_int` method. It actively tries to adopt what is helpful to the developer. Ruby is another language that gets this right.

Did you write `is_writeable` instead of `is_writable`? Don't worry, they're both [aliases to each other](https://www.php.net/manual/en/aliases.php)[^4]. Other aliases include:

|A|B|
|---|---|
|`join`|`implode`|
|`array_key_exists`|`key_exists`|
|`is_int`|`is_integer`|

Aliases are just the starting point. I've already mentioned the `base_convert` method, but PHP is filled with functions where it goes the extra mile to make your work easier:

|Function|Description|
|--------|-----------|
|[natsort](https://www.php.net/manual/en/function.natsort.php)|Sort an array using a "natural order" algorithm|
|password_hash|Creates a password hash|
|password_verify|Verifies that a password matches a hash|
|is_infinite|Finds whether a value is infinite|
|exif_read_data|Reads the EXIF headers from an image file|
|get_meta_tags|Extracts all meta tag content attributes from a file and returns an array|
|krsort|Sort an array by key in reverse order|
|array_change_key_case|Changes the case of all keys in an array|
|filter_var|A multipurpose way to sanitize, filter, validate user input. Let you validate/sanitize for valid domains, emails, IP addresses, MAC addresses, regexes, URLs etc.|

Here's how you check whether a string contains a valid MAC address in PHP:

```php
filter_var($mac,FILTER_VALIDATE_MAC)
```

This is the Python equivalent ([top answer on StackOverflow](https://stackoverflow.com/a/7629690/368328)) that doesn't cover EUI-64 format addresses (`0123.4567.89ab`):

```python
re.match("[0-9a-f]{2}([-:]?)[0-9a-f]{2}(\\1[0-9a-f]{2}){4}$", x.lower())
```

Want to check whether a domain name is correct? The following checks against RFC 1034, RFC 1035, RFC 952, RFC 1123, RFC 2732, RFC 2181, and RFC 1123.

```php
filter_var($domain,FILTER_VALIDATE_DOMAIN)
```

Python has a [third-party-module](https://stackoverflow.com/a/45011112) for the same, which marks domains with [underscores](https://github.com/kvesteri/validators/issues/102) or [trailing dots](https://github.com/kvesteri/validators/issues/141) as invalid. Python isn't alone here, the most popular [npm module](https://github.com/miguelmota/is-valid-domain/issues/13) only started to recognize underscores as valid in 2020. Ruby fails similarly here.

There's always an implicit trust in the correctness of standard-libraries, and having all of these correct implementations easily available in the base installation is a big win for developers.

As another example, PHP has been providing libsodium as a default extension since 2017 (7.2.0).

## Worse is better

The PHP standard library focuses on breadth instead of depth. It covers so much (as seen above), but simplifies everything it does. As an example, see the approach it takes for parsing INI files:

> [`parse_ini_file`](https://www.php.net/manual/en/function.parse-ini-file.php)
> <br>parse_ini_file() loads in the ini file specified in filename, and returns the settings in it in an associative array.

Python has a corresponding `configparser`, but it returns a `ConfigParser` object, which is more complicated to iterate through. Most importantly, it partially implement dictionary lookups, so while you can create configparser from dictionaries, configparser only pretends to behave like a dictionary. It breaks in some minor ways, which are now left for the developer to work through:

![](/img/pvp/python/configparser.jpg)

PHP on the other hand says: this is how PHP parses INI files. Here are a few knobs to let you automatically convert `"false"` to `false`, or parse multiple-sections. The function returns `false` on failure. (The python module has 11 exceptions it can raise).

Think of the complexity difference between these 2 approaches. The documentation for the python module is at 850 lines. There are 20+ functions in the configparser class. For something as simple as parsing INI files, should a developer have to worry about all of that?

By keeping the core standard library diverse and simple, PHP enables developers to worry about complications only if you need them, not by default. In other words: *cover 90% of the usecases with as little complexity as possible in the standard library*.

## Cute Constants

Ever wondered how do you write infinity in Python? Stackoverflow says:

>There is no way to represent infinity as an integer in Python. This matches the behaviour of many other languages. However, due to Python's dynamic typing system, you can use float('inf') in place of an integer, and it will behave as you would expect.

with a comment mentioning that Python 3.5 brings `math.inf` as a constant[^5]. This is likely why Numpy has its own `np.inf` constant.

PHP has the following supported since the earliest releases:

`pi, e, log(e, 2), log(e, 10), log(e, 2), pi/2, pi/4, 1/pi, 2/pi, log(pi), e, INF, NAN` (and a few more)[^7]

## Releases

If you search for "Python releases", the first result will point you to `python.org/download/releases/`, which has the following text:

```
Python releases are now listed on the downloads page.

This page only provides links to older releases which are not listed in the release database.

    Python 1.6.1 (September 2000)
    Python 1.5.2 (April 1999)
    Older source releases
    Python 1.5 binaries
    Python 1.4 binaries
    Python 1.3 binaries
    Python 1.2 binaries
    Python 1.1 binaries
```

This is how the linked download page looks like:

![](/img/pvp/python/releases.jpg)

And this is the corresponding PHP page

![](/img/pvp/php/downloads.jpg)

There are 2 important differences:

### Figuring out the the latest release

Python 3.8.2 is unsupported once Python 3.8.3 was released, but that page doesn't tell you what is the latest release in any given branch. For that you can scroll a table below (which also lists unsupported releases), or go to the PEP for that specific release, and look at its schedule to find out what was the latest released version. The table on that page with all releases can't be trusted:

![](/img/pvp/python/table.jpg)

It lists 2.7 releases alongside unsupported 3.8 releases. There is a nice header at the top that misguides you even further:

![](/img/pvp/python/header.jpg)

Clicking on Linux takes me to the [/downloads/source](https://www.python.org/downloads/source/) page which lists these 2 together:

- Latest Python 3 Release - Python 3.8.3
- Latest Python 2 Release - Python 2.7.18

No mention of 3.7 releases (still supported), or the fact that 2.7 releases are not supported anymore.

### Figuring out the End of Life

The PHP supported versions page is a thing of beauty[^8]:

![](/img/pvp/php/releases.jpg)

Figuring out the same information for Python takes a lot of clicks and efforts (or you could go to `endoflife.date/python`). While the EoLs are clear, the boundary when a bugfix branch changes to a security branch is unclear unless you lookup the specific PEP for that Python release.

TODO:

- packaging correctness. Mention how wordpress, woocommerce, and magento all use the same packaging system despite it being relatively nascent in terms of PHP's lifespan. Python fucks up bad OTOH.
- Maybe cover [PSRs](https://www.php-fig.org/psr/)?
- Templating?
- filestructure is your friend (you require files!)
-

[^1]: If you've been procastinating, there's a PHP project called [get-shit-done](https://github.com/viccherubini/get-shit-done) that you should check out.
[^2]: These are via DuckDuckGo, since Google's results are entirely compromised by geeksforgeeks, tutorialspoint, and w3schools.
[^3]: The Zen of Python says: "There should be one-- and preferably only one --obvious way to do it.", but the language disagrees.
[^4]: If you want consistency in your codebase - use a linter to pick one,
[^5]: PEP8 says [that constants should be capitalized](https://www.python.org/dev/peps/pep-0008/#constants), but we'll ignore that for now.
[^6]: 3.5 was released just in 2015, for reference.
[^7]: `e` is the newest constant here and was added in PHP 5.2 (released 2008).
[^8]: I created [endoflife.date](https://endoflife.date/) inspired by that page, and how much other projects get it wrong.
