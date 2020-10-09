---
layout: page
title: EBooks
permalink: /ebooks/
---

A fun side-project that I often pick up is generation of semantically correct ebooks from various online books and content.

## Books

Here's a list of the interesting books I've covered:

## Non Fiction

[Never Say You Can’t Survive][nsycs] [[source][nsycs-source]]
: Ebook generated from Never Say You Can’t Survive, by Charlie Jane Anders. Being serialized at tor.com, currently in progress.

[Site Reliability Engineering][sre] [[source][sre-source]]
: Google's book on Site Reliability Engineering. Published by Google as a online read under CC BY-NC-ND 4.0

[The Site Reliability Workbook][sre] [[source][swe-source]]
: The Site Reliability Workbook is the hands-on companion to the bestselling Site Reliability Engineering book and uses concrete examples to show how to put SRE principles and practices to work. Published by Google as a online read under CC BY-NC-ND 4.0.

[Security Engineering — Third Edition][se3] by Ross Anderson [[source][se3-source]]
: Comprised of the third-edition, currently under review PDFs. Only available till it goes to press.

## Fiction

[The Ickabog][ickabog] [[source][ickabog-source]]
: EBook generated from The Ickabog, written by J.K Rowling, and published online in seralized format.

[Hoshruba][hoshruba] (Translated by Musharraf Ali Farooqi) [[source][hoshruba-source]]
: Tor's serialized publication of Hoshruba-The Land and the Tilism. This is just Vol 1 of the planned translation of the famous persian epic, [Hamzanama](https://en.wikipedia.org/wiki/Hamzanama).

[Magic Muggle][mm] [[source][mm-source]]
: Harry Potter fan-fiction about a muggle going to Hogwarts. (3rd book ~~ongoing~~ abandoned)

I also went around converting [all of the original fiction published on Tor.com][tor-original-fiction] using [url-to-epub].

### Brandon Sanderson

[Rhythm of War][cosmere] [[source][row-source]]
: (In Progress). Initial chapters from Rhythm of War, Book 4 in the Stormlight Archive, being published by Tor in serialized format.

[Oathbringer][cosmere] [[source][oathbringer-source]]
: Chapters 0-32 from Oathbringer, Book 3 in the Stormlight Archive, being published by Tor in serialized format.

[Warbreaker Prime: Mythwalker][cosmere] [[source][mythwalker-source]]
: Initial draft of the Warbreaker by Brandon Sanderson, before various parts of it were incorporated into Mistborn.

[Way of Kings Reread][cosmere] [[source][wok-source]]
: Tor re-read of Way of kings, Book 1 in the Stormlight Archive.

[Words of Radiance Reread][cosmere] [[source][wor-source]]
: Tor re-read of Words of Radiance, Book 2 in the Stormlight Archive.

[Oathbringer Reread][cosmere] [[source][oathbringer-reread-source]]
: Tor re-read of Oathbringer, Book 3 in the Stormlight Archive.

[Edgedancer Reread][cosmere] [[source][edgedancer-source]]
: Tor re-read of Edgedancer, a novella between Books 2 & 3 in the Stormlight Archive.

[Defending Elysium][cosmere] by Brandon Sanderson [[source][de-source]]
: Brandon Sanderson's short story, part of the Skyward universe. Published on his website.

[Skyward][cosmere] by Brandon Sanderson [[source][skyward-source]]
: Chapters 1-15 of the book. Published at getunderlined.com.

Things next on my list:

-   <https://www.tor.com/series/warbreaker-reread-brandon-sanderson/>
-   White Sand (From .doc to EPUB)
-   <https://www.tor.com/series/malazan-reread-of-the-fallen/>
-   <https://www.tor.com/series/a-read-of-ice-and-fire/>
-   <https://www.tor.com/series/jonathan-strange-mr-norrell-reread/>

I only provide the scripts for the generation on GitHub. If you'd like a copy without having to run the script, [get in touch][contact] and ask.

## Tools

To help me in these various projects, I've ended up some tooling:

[muse-dl][muse]
: Wrote a crystal app to support downloading and stitching of books from [Project MUSE](https://muse.jhu.edu/). Project MUSE is a leading provider of digital humanities and social science content for the scholarly community around the world, run by the Johns Hopkins University. This generates well-polished PDFs with proper metadata.

[epub-metadata-generator][emg]
: Generates a metadata.xml file for an EPUB from various online sources, can be used with pandoc.

[url-to-epub][url-to-epub]
: A simple zero-config script that generates a standards-compliant EPUB from a webpage. Zero config. Requires pandoc

## References

Here are links to other similar tools that you might like:

-   <https://github.com/iarna/fetch-fic>
-   <http://ficsave.xyz/>
-   <http://ff2ebook.com/old/>
-   <https://github.com/sainathadapa/reddit2mobi>
-   <https://doocer.com>, which generates EPUB/MOBI files out of RSS/ATOM feeds, and given a TOC. Pretty cool
-   [Calibre Recipes](https://manual.calibre-ebook.com/news_recipe.html), which are similar but mostly focused on news websites instead of online books.

As a side-effect, I often get into the rabbit hole of generating the perfect EPUB instead of actually reading them.

[cosmere]: https://github.com/captn3m0/cosmere-books
[hoshruba]: https://github.com/captn3m0/hoshruba
[sre]: https://github.com/captn3m0/google-sre-ebook/
[mm]: http://github.com/captn3m0/magicmuggle
[contact]: /contact/
[se3]: https://github.com/captn3m0/security-engineering-ebook
[row-source]: https://www.tor.com/series/rhythm-of-war-brandon-sanderson/
[mythwalker-source]: https://www.brandonsanderson.com/warbreaker-prime-mythwalker-prologue/
[oathbringer-source]: https://www.tor.com/series/oathbringer/
[wok-source]: https://www.tor.com/features/series/the-way-of-kings-reread-on-torcom/
[wor-source]: https://www.tor.com/series/words-of-radiance-reread-on-torcom/
[oathbringer-reread-source]: https://www.tor.com/series/oathbringer-reread-brandon-sanderson/
[edgedancer-source]: https://www.tor.com/series/edgedancer-reread-brandon-sanderson/
[wokprime-source]: https://brandonsanderson.com/chapters-from-the-original-draft-of-the-way-of-kings-available-in-anthology-to-benefit-robison-wells/
[hoshruba-source]: https://www.tor.com/series/hoshruba-series/
[mm-source]: https://old.reddit.com/r/magicmuggle/
[sre-source]: https://landing.google.com/sre/sre-book/toc/index.html
[swe-source]: https://landing.google.com/sre/workbook/toc/
[de-source]: https://brandonsanderson.com/defending-elysium/
[tor-original-fiction]: https://www.tor.com/category/all-fiction/original-fiction/
[skyward-source]: https://www.getunderlined.com/read/excerpt-reveal-start-reading-skyward-by-brandon-sanderson/
[url-to-epub]: https://www.npmjs.com/package/url-to-epub
[se3-source]: https://www.cl.cam.ac.uk/~rja14/book.html

[muse]: https://github.com/captn3m0/muse-dl
[emg]: https://github.com/captn3m0/epub-metadata-generator
[ickabog]: https://github.com/captn3m0/ickabog-ebook
[ickabog-source]: https://www.theickabog.com/home/

[nsycs]: https://github.com/captn3m0/never-say-you-cant-survive
[nsycs-source]: https://www.tor.com/series/never-say-you-cant-survive-by-charlie-jane-anders/