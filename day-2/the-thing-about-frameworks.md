# The Thing About Frameworks
Tim Kadlec @ tkadlec, works at snyk

As a kid he really wanted to go to a Packers football game. He dresses up for it, but had to leave early from his first game because of the cold. His parents took him to get a souvenier on the way out. He got his tounge stuck on a cold object, his parents thought he could not make up his mind and pretended to leave to try and force him to make a decision.

He was feeling choice paralysis from all the different things in the shop. (Same thing happens when you try to pick a movie from netflix). There is a sense of being overwhelmed. This happens in javascript framework selections.

This would get called JavaScript Fatiuge, several blog posts have been written about it.

"Knowing what matters and what doesn't is a critical skill" 

jquery is on 80% of the top 10000 websites. other frameworks are on less than 1%.

Everything has a cost

1. we need to critically evalutae if we need a framework *at all*
  * browser looks for html, css, and js 
    * the js is a bottleneck, the parsing has to be paused while the js is downloaded and executed
      * async will continue to parse while the download is happening (but pause for execution)
      * defer will continue to parse while the download is happening and execute one all parsing is finished
      * avg page is sending 500KB of compressed JS

you need to worry about both compressed and uncompressed size. compressed size only matters when sending it over the network. The browser still has to parse and compile the uncompressed full javascript file.

Accessibility tree (?)
chrome has an accesibility expierement that lets you see the accesibility tree

some frameworks like Angular, can help address acessibility concerns.

maintenance is another cost, you have to keep these up to date to prevent vulnerabilities.

accessibility/sercurity/maintenence/learning they are all costs. we cannot just chase after the new things. There is no one-size-fits-all solution. 
