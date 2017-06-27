# Of Monoliths and Microservices: Adventures in Structuring a Web App
Shane Russell, United States Digital Service

department of veterns affairs has a github repo

software architecture is organic, things change. The decision to move to microservices moves one service at a time.

"Want better apps? Make smaller things." - Sandi Metz, All the Little Things

microservices make it easy to change one services without changing the others. However it makes updates to the whole system difficult.

Microservices should not have shared code, the whole point is to decouple them, not keep them close together. 
It is easy to move small methods and small classes, but a huge pain to move small services.

Continuous Integration was done with Travis CI and Jenkins

Conway's Law:
Any organization that designs a system will produce a design whose structure is a copy of the organization's communication structure.

Microservice applications tend to not get updated as frequently and can become old men. You are confident with no new code changes there are no new bugs being introduced, but there may be security vulnerbilities, or the logging is not up to par with the rest of the application.
