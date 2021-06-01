# Google Dorking


## Crawlers

**Crawlers** discover content on the internet through various means. One way is by pure
discovery, where a URL is visited by the *crawler*, and information regarding the website
is returned to the search engine.

Once a crawler discovers a domain, it will index the entire contents of the domain,
looking for *keywords* and other miscellaneous information, and stores them 
into a *dictionary*.

Another method of discovery is by following any URLs found on the original website, 
and any information found on the new website is also sent to the search engine. 
Crawlers are much like a virus in that they want to *traverse*, or spread to everything 
they can. Termed as **crawling**, they traverse every URL and file they can find.

Questions:
* Name the key term of what a "crawler" is used to do:
    - `index`

* What is the name of the technique that "Search Engines" use to retrieve this info about websites?
    - `crawling`

* What is an example of the type of contents that could be gathered from a website? 
    - `keywords`


## Search Engine Optimisation

**SEO** -- Search Engine Optimisation -- domains are *prioritised* on how easy they are to index

Influences on how *optimal* a domain is:
* how responsive your website is to different browsers -- includes mobile platforms
* how easy it is to *crawl* through sitemaps
* what kind of keywords your website has

Websites are *point-scored*, or ranked, and you can pay to have a site advertised/boosted

see [Google's Site Analyser](https://web.dev/)


## Robots.txt

Defines the permissions crawlers have to a website
```text
User-agent: *
Allow: /

Sitemap: http://mywebsite.com/sitemap.xml
```

Some Keywords:
* `User-agent` -- specifies the **types** of crawlers that can index your site
* `Allow` -- the directories/files that crawlers **can** index
* `Disallow` -- the directories/files that crawlers **cannot** index
* `Sitemap` -- provides a reference to where the sitemap is located

Note that Regular Expressions or **Regex** work here too:
```text
User-agent: *
Disallow: /*.ini$

Sitemap: http://mywebsite.com/sitemap.xml
```

Questions:
* Where would "robots.txt" be located on the domain "ablog.com"
    - `ablog.com/robots.txt`

* If a website was to have a sitemap, where would that be located?
    - `/sitemap.xml`

* How would we only allow "Bingbot" to index the website?
    - `User-agent: Bingbot`

* How would we prevent a "Crawler" from indexing the directory "/dont-index-me/"?
    - `Disallow: /dont-index-me/`

* What is the extension of a Unix/Linux system configuration file that we might want to hide from "Crawlers"?
    - `.conf`


## Sitemaps

Similar to real-life geographical maps, but for websites

Sitemaps specify the **routes** crawlers should take in finding nested content

The presence of a sitemap holds a fair amount of weight in the *optimisation* of a website

Think of it as using a wordlist to find files instead of randomly guessing their names

Questions:
* What is the typical file structure of a "Sitemap"?
    - `xml`
* What real life example can "Sitemaps" be compared to?
    - `map`
* Name the keyword for the path taken for content on a website
    - `route`


## Google Dorking

Using Google for *Advanced* Searching:
* using arithmetic operators: `12 + 1`
* using quotes: `"american psycho poster"`

Some Google Dorking Keywords:
* `filetype:` -- search for a file by its extension (ie: PDF)
* `cache:` -- view google's cached version of a specified URL
* `intitle:` -- the specified phrase **MUST** appear in the title of the page

Questions:
* What would be the format used to query the site bbc.co.uk about flood defences
    - `site:bbc.co.uk flood defences`
* What term would you use to search by file type?
    - `filetype:`
* What term can we use to look for login pages?
    - `intitle: login`


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
