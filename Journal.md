

# What is a Journal? #
Journal is by default a very simple class, which can be modified quite extensive to produce a complex set of rules for the crawler to follow. You can either subclass the default `Journal` class or you can create a new object with the three methods required by the crawler (see below).

## How it works ##
To create an instance of the `WebCrawler` class, you need to create a Journal-like object and give it as parameter to the crawler. The crawler will then save this object internally and revoke it whenever a user-made decision or action is required. Basically the crawler asks for this... :

  * **How many threads should live?**
> When starting the crawler using `WebCrawler.start()` the `thread_count()` method of the `Journal` object is revoked by the crawler. This method should return the amount of spider-threads alive when crawling. All non-integer/float values returned will raise an exception.

  * **What URL should I crawl next?**
> Every time the crawler is ready to crawl a new URL, the `nextUrl`-method of the `Journal`-object is revoked. This method should either return the next URL to crawl, or `None`. Sometimes it's necessary to return `None` (eg. when starting with a single URL, no more URLs will be available before the first page has been downloaded and parsed). The crawler will stop crawling when there is no spiders left alive and `nextUrl()` returns `None`.

  * **Parsing the page**
> Every time the crawler has finished downloading a page, the `parse`-method of the `Journal`-object is revoked by the crawler with a `HTMLDocResult`-object as only parameter. This object holds a couple of methods and members to extract some basic data from the page, like title, meta-elements and links. For example, using `HTMLDocResult.getLinks()` will return a list of links found on the page (relative URLs is converted to fully qualified URLs). The Journal must keep track of these links and give them back to the crawler through `Journal.nextUrl()`.

## The default Journal-object ##
The default `Journal`-object implements (probably) the easiest way of feeding URLs to the crawler and keeping track of URLs already crawled. It holds three private members for storing URLs:

  * A list of URLs not yet crawled
  * A list of URLs being crawled right now
  * A list of URLs already crawled

When the crawler revokes the `Journal.nextUrl()` method, the default `Journal`-object simply pop and return the first element of the list of URLs not yet crawled. The URL is appended to the list of URLs being crawled right now.

When the crawler then revokes the `parse()` method, the default `Journal`-object will then remove the URL from the list of URLs being crawled right now, and append it to the list of URLs already crawled. By using the `HTMLDocResult.getLinks()` method to extract all links found on the page, `Journal` will save the links using `self.add(url)`.

The default `Journal`-object also implements two methods to save and reload progress info: `Journal.dumpState()` and `Journal.loadState(s)`. `dumpState()` will simply pickle the three above mentioned lists and return the pickled string, while `loadState(s)` will simply unpickle the string given and save the data into `self`.

See a couple of [the examples](Examples.md) for a demo on subclassing the default `Journal`-object.

# Writing your own Journal from scratch #
See [the example here](Examples#Writing_your_own_Journal_from_scratch.md).