### Dean Hume, @ deanohume, works for Settled

  * accessbile on any device
  * fast

## Basics of Progressive Web Apps
  "These apps are just websites that took all the right vitamins."
  The use a website, a service worker, a minfest file, and run over HTTPS
  The service worker routers web page requests.
    The intercepts any request, they can reourte them, drop them, edit them, so-on.
    They are the key to unlocking the power in your browser
    If the browser doesnot support them, the browser will just fallback.
## Fast
   ### Caching
     First visit, cache all the resources a user needs
     Register the service worker, then begin grabbing all the resources the user will need and store them.
     If the incoming request matches anything in the cache, then just return what is in the cache instead of actually going to request that resource. 
     Once the service worker was implemented, page load times went from bout 4.5s to 500ms. page weight went from 850kb to 50kb
   ### HTTP2
     With multiplexing, you can just open 1 TCP connection, and request multiple resources over it.
   ### Techniques
     They used no javascript frameworks.
     Render pages on the server.
     HTTP2 Push
       * resources are sent with the initial request for the HTML
     brotli is an alternative to gzip, its worst case compression is 10%
## Reliable
   Network first approach, if the user is offline, the service worker will user the cache.
   Test your service worker code
## Look and Feel
  ### Manifest file
    tells the browser what your app is about
      * on mobile - can change url bar color
      * specify icon
  ### add to homescreen
