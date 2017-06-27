# Automating Peace of Mind with Accessibility Testing & Continuous Integration
Marcy Sutton @MarcySutton
Senior Front-Eng Engineer, Deque Systems
Slides: http://bit.ly/a11y-and-ci

Accessibility Meetup?
egghead website has an accessibility course (made by Marcy)

Send Marcy any accessibility wins, she wants to hear about them.

Function testing
  unit testing
  integration
  system
  acceptence
non-functional
  performance
  ....

## Accessibility Testing
  HTML/ARIA validation
  Forma validation
  color contrats
  accessible naming
  focus management (testing that focus works correctly)
  specifying a language

  focus order
  text alternative quality
  screen reader testing
  keyboard support
  contrast over images/gradients
  error identification

How are people affected (people can fit into multiple buckets)
  visual
  hearing 
  motor
  cognitive

Automated tests can catch roughly %30-%50 of a11y issues. These are things we dont need to waste developers times on.

Accessibility Unit Tests
Good For
  * Componenet-specific behavior
  * Intearction/focus APIs
  * Text alternatives
  * ARIA states

Integration/E2E Tests (like with selenium using a real browser)
Good for:
  * Real-world browser testing
  * Document/page-level rules
  * Widget interrop
  * Color contrast
  * Framework testing options

Get with an Accessibility Testing API
aXe-core is an engine for testing accessibility.

aXe-CLI can be instlled can be used via the command line for more control

`circle ci` `travis ci`

By having sufficient test coverage, you will know when you break accessibility and be able to prevent it
