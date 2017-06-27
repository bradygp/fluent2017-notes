# Automating Performance Testing in Pre-production
Billy Hoffman billy.hoffman@rigor.com, works at Rigor

We should be able to catch problems before they get to the user
Performance Problems == Bugs

Book: High Performance WEbsites
If you are using SSL, you *should* be using HTTP2

Testing For:
  UX Metrics
    Speed Index
    Start Render
    Visually Complete * - Can be tricky to define (like with a hero video)
    DomContentLoaded
    OnLoad
    FullyLoaded
    Custom Timings
    Custom Industry/Company Metrics
      Time to First Ad
      Time to Active All-To-Action (Time to when user clicks on question?)

  Performance Budget
    Total Content Size
    Content Size by Type
    Content Size by origin (1 party content vs 3rd party content)
    different devices

  Specific Problems
   *there was a list*
   you can shrink down images in the web browsers, but if you shrink them ALOT, then just make a smaller one and show that

How do you know when to fail?
 there is nuiances to this, but tools like pagespeed and webpagetest will help you determine this

**You do not care about the change between each build, you care about the longer change over time**
Checking the last build is just a sanity check, it is ok to be slightly off.
You should be close to the trailing 3 day median
Compare the perforamnce against 4-6 weeks ago, and 3 months ago.

## How do you do all of this
phantomjs has a lot of problems, do not use it
host your own instance of webpagetest

1. staging
  stable pre-prod environment
  very similar to production

  have an emulated network
  with webpage test, do run 9 concestivie test, not the default 3.
  staging will never be exactally like production?

His company made apitester.com a website for automating the testing of APIs
