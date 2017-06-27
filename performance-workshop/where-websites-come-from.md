Class is using twitter hashtag `#fedebug`

url goes to the network
looks for html/js/css asset types
  uses this to build a DOM and CSSOM
  goes to render tree, layout, then paint

Latency - time it takes to get from A to B
Bandwidth - how much can you fit in a pipe?

Bandwidth is cheap and easy to manufacture

paper: "It's the Latency, Stupid" http://standord.io/22wyp7m
akamai has a state of the internet report, bandwidth has been increasing.
Once you have bad latency, you are stuck with it.

### Example
Send request 4148KM
light travesl at 300K KM/s
14 ms to send request at speed of light (in vacume) 
in fiber, it's more like 21ms one-way, or 42ms two-way
If you ping the server, it will still be even longer than this. Your connection gets routed through different hardware, and every step has different delay
`traceroute` command will show all the different stops along the way. This helps to give you a good idea of latency.
As bandwidth improves, there is an increase in latency, but it can only help so much before all the bandwidth in the world won't do any additional help
If you are able to lower the latency there is a linear decrease in pageload times.

DNS Lookup + TCP Connection + SSL Negotiation + Time to first byte + content download

## DNS Lookup
take the domain name and resolve it into an ip address. 
It can happen at multiple layers
browser cache/os cache/router cache/isp dns cache/ recursive search
browser cache is basically nothing, recursive search is the longest if it is not in any of those mentioned caches.

CHROME://DNS
 * Webpagetest video - https://www.youtube.com/watch?v=6UeRMMI_IzI&index=7&list=PLWa0Ky8nXQTaFXpT_YNvLElTEpHUyaZi4
 * Webpagetest video - https://www.youtube.com/watch?v=euVYHee1f1M&index=8&list=PLWa0Ky8nXQTaFXpT_YNvLElTEpHUyaZi4

## TCP Connection
3-way handshake 
Client     Server
SVR     ->
        <- SVR ACK
ACK     ->

## SSL Negotiation
 client hello ->
  <- server hello
key exchange(?)  ->
 <- key exchange (?)

## Request
SYN, GET /file ->  # TCP slow-start: gradually making sure bandwidth is avaliable before using that bandwidth, The amount returned is configurable on the server. Should default to return 10 segments
<- server sends back 4 segments of TCP data
-> ACK 4
<- sends 8
-> ACK 8
<- sends 16
-> ACK 16
so-on, and so-on
If you uses a cdn or load-balancer then you have to worry about this configuration between the client and the cdn/load-balaner (not your server)


It is suggested to use a CDN, they optimize for performance and are distributed to be close to the end-user.
Use `keep alive` once a TCP connection has been established, it can be reused, without needing to go through the slow-start.
should be in htaccess of apache configs
```
KeepAlive On
<ifModule mod_headers.c>
Header set Connection keep-alive
</ifModule
```

### [Resource Hints](https://w3c.github.io/resource-hints/)
Is a set of standards
 * can be done as `header` link for css
 * could be a link element in the page `preload`
 * can be added via javascript (this is not really done, but if you want it programatically done, it is possible)

 * `dns-prefetch` - takes care of the DNS Lookup, it has a *very* small to no difference. It takes care of the DNS Lookup for that resource. 
   * There is no down-side to using it
 * `preconnect` - Does the same thing, but does not have as good support, it takes care of the DNS Lookup, TCP Connection, and SSL Negoitation.
   * google fonts does this. 
   * happens asynchronously as soon as the browser parses the <head> that has this loaded in it
   * can use both `dns-prefetch` and `preconnect`
 * `preload` - this is about a specific resource, it can do the same as `preconnect` but also do the request
 * `prefetch` - same as `preload` except it gets something in preperation for the next pageload (used within the next 2-3 navigations)
 * `prerender` - very little support. Basically opens up an invisible tab of that page. When the users goes to that page, it is already fully loaded.
   * orgs would try to prerender too many pages and it would crash the browsers.

preload, prefetch, preender actually pull back assets, and are therefore the most data-intensive ones.

 * a downside to combining everything, if a obscure change is frequently made in css. The combined css file gets changed and keeps getting kicked out of the cache.
  * consider network cost, cacheability, and other things.

The browser has 2 parsers, the main html parser. 

As the HTML gets parsed, a tree is made with elements containing what is inside those html elements. Comments are in the HTML DOM. 

CSS is render blocking. If the css link element has a media object, if it does not apply, it will not block render.
JS is able to mess with both the DOM and CSSOM. 
JS is not just render blocking, it is parser blocking.

CSS Blocks JS Execution
JS Execution Blocks DOM Parsing

`async` and `defer` are script attributes.
* `async` wont stop DOM parsing, and will execute the script once it has been retrieved. 
  * this has a problem with race conditions and JS dependency management, there are javascript loaders that help solve this problem
* `defer` wont execute any of the script until the DOM has been fully built.
  * `defer` and placing the script and the end of the document, will basically be the same thing.
  * If the Javascipt is doing something to the DOM, then leave it blocking, defer is meant for things like google analytics, or something that doesnt affect the user at all.
  * if it afects the display of the page, you dont want to defer it
Book: High Performance Websites
Book: Designing for Performance:
Book: Illyas Performance book (it is very intense)

#### Andy & Bills Law
 - whatever Andy gives, Bill takes away.

Render tree looks at the DOM and CSSOM. Render tree contains visual and markup information, only things that will be displayed (no head, no comments, etc.)

The criticial path is the first network connection to painting.

## How to shrink a critical path
 * html is a critical resource
 * style sheet is in the critical path
   * tricky to use css
   * you can write inline-css for what the user *very first* sees on the page load (still keep the css in the css files)
     * by inline, it means inline block css (a style block at the top/bottom of the page)
     * critical css task in grunt and gulp that can identify the critical css (loaded without scrolling)
     * may best do these on question list page, and question page. 
     * akamai also has an analyzer for critical css
 * javascript is in the critial path
   * can use async, defer, or a script loader

### Fonts
if you use a webfont *just* for a brand logo, you can specify the text in the request and will decrease the request size. 

### Images
It is tempting to think puerly in file size. It is something to consider, but it is not the only thing.
When creating a jpeg, it goes through a process. 
 * RGB -> YUV
 * Chroma Subsampling
 * DCT/Quantization
 * Huffman Encoding

A Browswer has to reverse this process to go from an image into RGB values.
Best rule is to resize images. 
 `srcset` is an img attribute to tell the browser which versions of the image at which size.
 The `sizes` attribute and what sizes to display the image at
 The `picure` tag will let you progressively enhance images with different sources of different sizes and different types (for different browsers)


# Resources
 * https://developer.akamai.com/learn/FEO/optimizationoverview.html
 * https://twitter.com/search?f=tweets&q=%23fedebug&src=typd
 * [Hero Image?](https://envato.com/blog/exploring-hero-image-trend-web-design/)
 * [Grunt Task for WebPageTest](https://github.com/tkadlec/grunt-perfbudget)
 * https://wpostats.com/
 * https://developers.google.com/web/progressive-web-apps/
