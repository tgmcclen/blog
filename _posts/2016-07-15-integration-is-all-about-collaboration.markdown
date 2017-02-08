---
title:  "Integration is all about collaboration"
date:   2016-07-14 19:46:20
---

It's a lesson I learnt early in my engineering career but often it can be hard to get the message across to others and something that I need to stay disciplined on adhering to myself.
 
Integration, whether it be system or data, between components in an organisation, is exclusively about collaborating with everyone (I mean literally everyone) you can think of who may have any interest in the components in play.  I've seen situations where collaboration between many of the impacted groups is had but not all are included.  The risk is somewhat diminished with each group in the mix but there is always a residual risk while ever all of them are not included.  
 
The reality is that you need to start with assuming that all these groups need to be consulted:

* Architecture
* Security
* Risk and Compliance
* Infrastructure
* Operations
* Application Delivery teams of impacted assets
* Related Business Owners of the impacted assets  

Not engaging with __ALL__ these groups increases your risk of something coming unstuck in your integration approach.  And there is every chance that the problem with the solution may not come to light until you are in production and then you can be a real pickle with a lot of frustrated stakeholders.

Important to note that working with all these stakeholders doesn't guarantee successful integration, but it does ensure that you have awareness and buy-in from all so when things don't appear to be working out how everyone hoped, you have a cohesive working group to help find the way forward.

It is not always practical and appropriate to involve all these stakeholders.  You should pair it back based on several factors:

* Integration pattern usage
  * The less common this type of integration pattern is between these components means more collaboration required!
* Usage of published APIs
  * If the producer has published and well documented APIs along with SLAs and an acceptable use policy then the consumer has little need to engage with the producer directly - but they need to ensure that they have consumed and understood all the information provided.  Organisations are getting better at this type of approach even for internal APIs (spurned on by the advent of [Micro Services](http://microservices.io/patterns/microservices.html)) but you would need to judge just how mature your organisation is at doing this.
   
And finally, this needs to be complimented with smart engineering practices like up front [Consumer-Driven Contracts](http://martinfowler.com/articles/consumerDrivenContracts.html), continuous integration testing, and lots of ongoing communication during the SDLC.
