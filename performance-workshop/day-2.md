# Measuring Performance

Synthetic and Real User measurement
Get more detail with synthetic, but you dont know for sure how users are expierencing your site.
Synthetic gives consistent results with lots of detail, real user varies a lot.

## Synthetic Measurement
Several services offer synthetic testing. The problem is 10% back-end resources and 90% front-end resources. 
Chrome Dev tools has ways to test with realalistic bandwidth constraints. 
Facebook ATC will run on linux to simulate different traffic levels
  * http://facebook.github.io/augmented-....

When doing synthetic testing, it is very important to use an *actual browser*
  * use the browsers that your users are using

## Real User Measurement (RUM)
  * measure every page they visit
  * no reference on how competitors are performing

window.performance.timing gave a *substiantial* amount of inisight into performance including handshakes.
Resource Timing will let you get a waterfall diagram for your end-users. It is written in JavaScript. 
`windows.performance` is the waterfall data, it is always recorded and very little performance impact in doing something with it

### User Timing
  * performance.mark('name')
  * performance.measure()
  * performance.getEntriesByType('mark')
  * performance.getentriesByType('measure')

Paint Timing - Not Launched (in a couple of weeks) Chrome, not firefox 
  * get the first time something non-white was painted
  * get the time first content was painted (not style)

performance observer - you can attach a listener for performance events, and wait for them to occur
long tasks - anything on the main thread that takes more than 50ms gives a callback.
  * 50ms is the magic number, and cannot be changed.

Server Timing (coming soon) - get header information. 

Good Analytics has Performance Metrics, but it is buried. Page Timings and User Timings.

## Application Performance Measurement (APM) 
This is back-end performance measurement. (Time to first-byte)
  * New Relic, ruxit, dynatrace

The `speed index` is a way of tracking how quickly and how much content gets loaded on the screen. 
  * speed index is recommeded to be 1000 or less
`lighthouse` will report time to interactive. When the javascript is loaded so the user can do stuff on the site.

# Diving Waterfalls
This is all from the webpagetest waterfall
If there is a lot of yellow, server is responding with 304 (not modified) and those could probably be modified
If there is a slow 'time to first-byte' there is a slow back-end and you need to fix that.
Base page redirect (first few yellow lines) These should be pretty instant. 
Any red bars are 400/500 errors
Keep-alives, first thing to go fix usually
large resources, try and optimize them (how?)
Bandwidth constraints - not unusual to have dips in bandwidth early on
DOM CONTENT LOADED HANDLER - this should always be a thinish pink bar
lots of requests - as a rule, if the thumbnail of your waterfall doesnt fit on your screen, it is too big. short waterfalls is good
vertical green line is start render
javascript execution - only works with chrome, a lot of orange is a lot of javascript activity

optimely is a javascript library for a/b testing. It is better to use their server-side code, because their client-side code causes substiantial performance hit.
in performance, 5 seconds in a cliff, if your page takes longer than 5 seconds, it might as well not load at all.

Using webpagetest it is possible to get a list of images the site loads in their actual sizes and resolution

## SPOF - Single Point of Failure
SPOF are resources (usually to 3rd party domains) that will block your website if they are down are having problems
you can use webpagetest spof settings to change those domains to a `blackhole` so they are basically unused and you can identify if they are a SPOF
have a timeout of under 20 seconds (its agressive) to better catch SPOFs. 
try to load all 3rd party resources async.

# Primary goal is not to get 100/100 on lighthouse or pagespeed insights, they are just guides.

## Performance Tab - Chrome Dev Tools
  * Red Horizontal bar on the top - frame rate dropped, something in that area took a long time to load.
    * the flame chart will have red arrows next to the problem areas. Usually youll need to follow the flame chart up to figure out the actual problem, because that is just the result of the actual problem
  * yellow is scripting, purple is rending

# HTTP2
  * TCP works best for long continuous flows of communictions. However sites communicate in short bursts of traffic.
    * instead of multiple resource requests, people would combine and minify them. however this would hurt cacheability of them.
  * Biggest feature is multiplexing. multiple file request can be sent out on the same connection and be recieved in any order.

HTTP2 uses binary framing. 
   * A return request contains 1 header request and possibly 1 or more data requests.
   * Each stream has a priority between 1-256 and can be dependent upon another stream.

Just turning on HTTP2, without any changes, sites report 0%-26% performance improvments.

## TLS
purple line in waterfall is TLS negoiation. Needs to be at most 1 extra round trip.
OCSP is the most common reason for HTTPS taking a long time.
certificates can be big, and there can be multiple ones. 
TLS False Start - what you really want to optimize for. 
The fasts TLS can go is the same as the previous segments in the waterfall diagram.

## Service Worker
  * Service Workser may have its own cache
  * on first page view they wont be active, dont assume they will always be there
  * iframes are not part of your document
  * HTTPS must always be on
  * they have no concept of a page or page load, all they see is a stream of inbound requests
  * everything must be done asynchronously
  * pretty much only firefox and chrome support.
  * can add listener for fetch events
  * offline progressive web apps
  * can do custom error pages
  * https://www.smashingmagazine.com/2016/02/making-a-service-worker/

# Resources
  * https://developers.optimizely.com/x/solutions/sdks/reference/index.html?language=php
  * https://umaar.com/dev-tips/
  * https://www.youtube.com/watch?v=obtCN3Goaw4
