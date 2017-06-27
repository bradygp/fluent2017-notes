# Reverse Engineering Amazong and the Guardian
### David Fox @theobto, CTO at LookZook.com, Contributor to Blink (Chromium)

Modern web-dev can feel like being in a labrynth. Amazon and the Guardian have successfully navigated this labryntith.

### Amazon v Walmart
Amazon loads the view port first, and it feels *substiantially* faster than the walmart page which technically loads more quickly.

# Gleaning Information

## TCP - The mailman of the internet
TCP Slow start is a way to test the waters for how much a user can recieve in a TCP packet. 
The average HTML page is 40kb, starting with 4kb slow start, this would take a minmum of 4 round trips to show anything. Across the country that is 70 ms of just an average html page with no js or css on the best ethernet.
By enabling `IW10` you start with 14KB and get down to 3 round trips, this is thinaks to google. This is enabled by default in newer linux kernels. 
`Transfer-Encoding: chunked` is a header to let the browser know your sending stream information (what kind of information?). This is a quicky and easy win.

Keep servers up to date, and try to stream responses when possible.

## Parser
Starts at the top and goes to the bottom, builds the DOM and the CSSOM then the render tree. The render tree is the browsers representation of the webpage. 
*CSS Blocks rendering. If the css is being downloading, the browser will not download anything*
Amazon/guardian use a library called `loadCSS` to loadCSS in a non-blocking way. This is not the best way, because it can get a bit clunky
Another way is The Module / Future Way
you can put the link element (for the stylesheet) right above the element that uses it (outside of the head). It will only block for that element and things below it (nothing above)

CSS Blocks JS execution (a JS block will not execute until any preceeding CSS blocks are run)
Use `async` and `defer` when possible.

## Goals on What to do
  * Quickly get *something* loaded to the user to confirm they are on the page they want to be on.
  * Allow users to acclompish their initial goal
  * load remaining content in order of importnatnce

## Resources
  * Dan Ariely - Predictably Irrational
  * Ilya Grigorik - High Performance Browser Networking
  * HTML5 Spec - Very well written for a spec

Slides for this presentation will be tweeted out
