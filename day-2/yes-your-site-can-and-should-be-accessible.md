# YES! Your site SHOULD be accessible: Lessons learned in building FT.com
Laura Carvajal - @lc512k

Accessbility doesnt just happen, you have to make it happen
Web accessibility means anyone can use the web
"Beyond not denying access, we need to make sure everything is fair to everyone" -- Speakers Daughter
There are permenant, temporary and situational dissabilitys (deaf, ear infection, bar tender)

We can start small

`npm install -g pally` detects some accessiblity problems in your marku
`pally-ci` is an automated accessibility tool

build would break if they introduced accessibility errors (no more of the automatically detectable ones)

## Train people

Color Contrast issues where very common problems
all text needs a 4.5:1 contrast ratio (pally can test for this) this was the most common error
Alt text issues was the second leading error. all images need alt text, we need to decide what it should be and how verbose it should be
  * decorative (sceneary)
  * convey information (relevant to the context around it)
  * convey *really* complex information (infographics, charts)
    * may be appropriate to embed a link (or provide a hidden link) with a description of the page
    * maybe use SVG instead of PNG, they have more accessiblity options
labels, use `for` to tie label to input.
required fields, put an * next to the label

Things on the screen that look the same, but arent, add context. (like menu buttons)
Udacity has a great class on Web Accessibility

pally can catach 20%-30% of errors. Once you get to 0, you still have a ways to go.
Get an external Audit
Do Customer Research
Use Accesibility tools like a screen reader, or keyboard only, etc.
  * voice over
  * keyboard only
  * invert screen colors
(do all of the above)

"It's the right thing to do" doesnt get you a budget
Diversity improves your product, your team, your life

