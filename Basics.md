

# Journal #
What is a Journal?

## Examples of customized Journals ##
Examples...

<br>
<h1>Request objects</h1>
What is a Request object?<br>
<br>
<h2>Members</h2>
Public members of the Request object:<br>
<br>
<b><code>str url</code></b>
<blockquote>URL to request, excluding query string.<br>
<b><code>str method</code></b>
HTTP request method<br>
<b><code>dict args</code></b>
HTTP query as dictionary</blockquote>

<h2>Methods</h2>
Public methods of the Request object:<br>
<br>
<b><code>__init__(url, method='GET', args={})</code></b>
<blockquote>Initialize the Request object<br>
<b><code>addHeader(name, value)</code></b>
Add a header to the HTTP request.<br>
<b><code>addCookie(name, value, **attrs)</code></b>
Add a cookie to the HTTP request.</blockquote>

<br>
<h1>Response objects</h1>
What is a Response object?<br>
<br>
<h2>Members</h2>
Public members of the Request object:<br>
<br>
<b><code>str url</code></b>
<blockquote>The requested URL<br>
<b><code>str html</code></b>
Response HTML. Is <code>None</code> when the page could not load (socket error)<br>
<b><code>dict headers</code></b>
HTTP headers returned by the server<br>
<b><code>str msg</code></b>
HTTP message returned by the server<br>
<b><code>int code</code></b>
HTTP status code returned by the server</blockquote>

<h2>Methods</h2>
Public methods of the Response object:<br>
<br>
<b><code>getCookies()</code></b>
<blockquote>Returns a list of cookies set by the server<br>
<b><code>getCookie(name, default=None)</code></b>
Returns the value of a cookie set by the server. Returns <code>default</code> when cookie name doesn't exist.<br>
<b><code>getTitle()</code></b>
Returns contents of the first occurrence of a <code>&lt;TITLE&gt;</code> tag, or <code>None</code> if no title-tag was found on the page.<br>
<b><code>getMeta()</code></b>
Iterate over dictionaries, where each represents the attributes of a <code>&lt;META&gt;</code> tag found on the page.<br>
<b><code>getLinks()</code></b>
Iterate over links found on the page. Yields <code>(target, tag, attributes)</code>.<br>
Example: <code>('http://some-url.com/some-link.html', 'a', {'target':'_blank'})</code>.</blockquote>

<br>
<h1>URLs</h1>
pywebcrawler is using the <b>lxml</b> module fetch links from HTML pages. lxml uses the URL in which a link was found as base URL, and pays attention to <code>&lt;base href&gt;</code> tags when converting relative to absolute URLs.