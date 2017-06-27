css dig is a chrome extension for evaluating css attributes used on a pagr, like font colors, z-index etc.
atoms -bare bones page needs
molecules - more complex elements
infrastructure - like layout or grid

naming with intent is important for thems (light/dark) rebranding, 

atom - 
  color
    primary color
    danger color
    success color
    divide colors (2)
    themes
    gradients (some variants of the other colors)
    primary text ensure 4.5:1 constrast ratio against all background colors) (color contract checker is a great tool for this)
    secondary text
    caption
    links
  font
  buttons
    primary action
    passive
    more...

molucule - 
  tabs - these have media queries for the proper dimensions, they also have the proper attributes for accessibilty
    vertical
    horizontal

structure - 
  vertical align
  flexbox
  grid systems


PostCSS will help build your style guide
`npm install postcss-style-guide

styleguide-starter-kit provides a boilerplate

`npm install -g styleguide-starter-kit`

It is important to ensure that the style guide grows and the product grows

`CSSStats CLI` allows you to check in your linting that your application conforms to your style-guide
`WAVE` is an accessibility tool that will overlay ontop of your site and higlight accessibliity problems


Ally style guide is a great online resoruce for accessibility
