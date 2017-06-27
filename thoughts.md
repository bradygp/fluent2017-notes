use shield colors as background color for tags
  * maybe orange for regular tags, and red for official tags

create a 2D shield with the same colors, use that as the shield icon
  * look into giving it a gradient or shiny candy coating

We should have a utility server
  * either MASH or BS, if BS the server will need to be upgraded ( i guess )
  * services include
    * npm proxy
    * backups
    * webpagetest instances
    * cron that pings production and emails whenever it is down

load all avatars as a default avatar, once the page is loaded, use javascript to to populate the real avatars (if they exist)
  * we should probably just lazy load the regular avatars instead
  * https://css-tricks.com/snippets/javascript/lazy-loading-images/

http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/

Docker container that monitors the rest of the containers and serves as an alarm system in case any of the other containers has a problem 

Regularaly backup docker volumes to S3
  allows for us to restore snapshots of them at any point
  acts as a backup
  can later be used for database load balancing

Integrate RT with tap.
  Allow users to give a Tap kudo from RT. We may only allow this to be done from the question asker to the author of the accepted answer (or something similar)

  DQ.com
  a11ywins.tumblr.com
  egghead.io # start building accessible web today 
  Carl Groves website
  webaim.org ()
  twittery #a11y
  #a11ycasts on youtube 

tech talks
  have them on a reoccuring AND regular basis (weekly or every other week?)
  every developer, including interns should be doing them (Tony?)
  talks can include front-end frameworks, accessibility, performance, testing, team management, best practicies, specific tools, combinations thereof
  (come of with a list of ideas for people to pick from, in case they arent sure of where to start?)
    * vue.js, preact.js, react.js, webpagetest, pagespeed, aXe-core, jenkins, travis-ci, kuberneties, firefox javascript debug, git, using a screen reader, phpunit, grunt, glup, bootstrap 4, HTTP2, TLS, OOP, php tips and tricks, js tips and tricks, 
