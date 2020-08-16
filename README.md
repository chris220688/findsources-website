# [FindSources](https://findsources.co.uk/)

<p align="center">
	<img width="200" height="200" src="https://findsources.co.uk/favicon.ico">
</p>


# Description

[findsources.co.uk](https://www.findsources.co.uk) is a website that serves as a search engine for books.

Users can register as authors and create their own references for any book they might have found interesting.

The search results are based on such references rather than the actual content of the books.

The vision is for this to evolve into a free 'indexing' service for books, with a plethora of references, that will not conflict with any of the authors' rights.


# Architecture

This is single page application that is using [ReactJs](https://reactjs.org/) (frontend) with a combination of [FastApi](https://fastapi.tiangolo.com/) microservices (backend).

The search is performed by an [Elastic Search](https://www.elastic.co/) cluster and the results are rendered using [ReactiveSearch](https://opensource.appbase.io/reactivesearch/).

The database of choice is [MongoDB](https://www.mongodb.com/) and the synchronization between the database and Elastic Search indexes is achieved using [Monstache](https://rwynn.github.io/monstache-site/).

Errors are reported using [Sentry](https://sentry.io/welcome/) and Continuous Integration is managed by [Github Actions](https://github.com/features/actions).


# Scalability

Though not the main concern, until it becomes the next "Bookiepedia", the website has been designed in a way that it could scale to support a potentially higher number of users.

The services are built with separation of concerns (SoC) in mind and run in a kubernetes cluster, with the ability to scale horizontally. It goes without saying that Elastic Search can do the same.

MongoDB performance should not be a real concern since the search queries are performed on the Elastic Search cluster and not directly in MongoDB. However, if the schema grows more complex in the future, MongoDb could be easily unplugged without effort and replaced by a more traditional SQL one (like PostgreSQL), as long as it respects the interfaces that are in place.


# Security

Security is always one of the main concerns. The website is designed in a way that it follows (or at least it attempts to follow) some of the best practices when it comes to authentication.

However, since one can never guarantee that this will always stand true, the amount of personal information that is stored in the system has been kept to a minimum, so that even if the system is compromised, important data will not fall into the wrong hands.

That does make it a bit harder to create a unique personalized environment for every user, but it is a small price to pay for keeping our user's information secure.

Again, the philosophy is "If you can't keep something safe, don't keep it at all".

That being said:
1. SSL is enforced, using Let's Encrypt certificates.
2. Authentication is performed using the OpenId Connect protocol, exclusively via Azure and Google.
3. HTTPS secure cookies are used for short life sessions.
4. Personal information is kept to a minimum and when necessary, stored encrypted in the database.


# SEO

Had I known more about this before, I would have probably opted out of the single page application idea. Even though Google bots are far more sophisticated at the moment, I still believe it will be a challenge to index enough content with the current architecture. Luckily, there are alternative solutions!


# Technologies

|Front End                                                        |BackEnd                                              |Other                                                           |
|:---------------------------------------------------------------:|:---------------------------------------------------:|:--------------------------------------------------------------:|
|[ReactJs](https://reactjs.org/)                                  |[FastApi](https://fastapi.tiangolo.com/)             |[Kubernetes](https://kubernetes.io/)                            |
|[ReactiveSearch](https://opensource.appbase.io/reactivesearch/)  |[MongoDB](https://www.mongodb.com/)                  |[Digital Ocean](https://www.digitalocean.com/)                  |
|Azure/Google OpenIdConnect                                       |[ElasticSearch](https://www.elastic.co/)             |[Sentry](https://sentry.io/welcome/)                            |
|                                                                 |[Monstache](https://rwynn.github.io/monstache-site/) |[Github Actions](https://github.com/features/actions)           |

# Acknowledgements

Special thanks to the creators of [FastApi](https://fastapi.tiangolo.com/), [ReactiveSearch](https://opensource.appbase.io/reactivesearch/) and [Monstache](https://rwynn.github.io/monstache-site/).

Keep up the great work!
# Authors
Christos Liontos
