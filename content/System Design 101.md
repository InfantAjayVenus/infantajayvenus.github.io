*tags*: #hld

---
## Introduction

System Design is the process of designing the infrastructural components of a software architecture such that it enables the software system to handle specific scenarios like high rate of requests, large data flows etc.,

Simply put, if software is the code that does something, System design provides us the a map of places to put that code so that it can achieve it's purpose.

## The Application
Let's try to design a system, where the application can handle certain scenarios well. The scope/use cases of the application itself is irrelevant, so is the technology the application is built on. 

For now let's assume this a simple client server application that has a front-end and connects to a back end through a series of APIs. Our design for now is going to focus on the back-end for the most part.

## The Design
We currently have our production backend deployed to a single server hosted in a popular cloud service, our users are happy with our application, they're sharing their experience with their peers. We're gaining more and more traction as the day goes.
To feed fuel to this opportunity, our marketing team has announced an extended free trial period which is causing a lot more users to sign up to our application.

### The Lone Server
All these users are opening the application and are clicking through it to explore, every click leads to one or more API calls to be fired to the backend server.
Our server seems fine till 100k requests come at a time (that's how good of a code we've writtent ;-} ). But the rapidly growing user base is increasing the load very fast and our server is maxing out it's CPU and Memory caps. Requests are getting dropped, users are seeing unexpected errors, the very thing we tried to improve our product's reach is trying to kill it. We need to fix this ASAP.

### Spreading
The scenario we currently are in, where the load is put through a single point is called `Bottleneck`.
So the server is struggling because the 48 CPU cores and 64 GiB RAM are getting overloaded? Let's ramp up those resources, after all, we have hosted in the world's best cloud provider!
So We have doubled the cores and the RAM of our server, we're good right?

Not exactly, what we've done now is called [[Vertical Scaling]].
Yes, the server can now handle much more requests, say 500k so we're good till then.
But what if our users get more enthusiastic about our app and our user base explodes even more? The most number of CPU cores in an AMD EPYC processor is 192 and the maximum RAM it supports is 6TB as of this writing, so there is a hard limit on this way of upgrading the server.

Even if not, right now our application is running a physical server in some data center, what if the data center lost its power, if it got flooded, if someone tripped over a wire and disconnected the network cable to our server (has happened for real)?
Our only server no matter how powerful it is will go down. This is what we call `SPOF`(Single Point of Failure).

Another way to approach this is, we can add another server to share the load of our lone server. This solves both our problems, if one goes down there's another to take over and there's no limit for the number of servers we can add. This is called [[Horizontal Scaling]].

### Whom should I ask?
So we agree that adding more servers is the better solution. But this has left us another problem to solve. Now that we have multiple servers, our front end wouldn't know which one to call.

Now there's two ways we can handle this,
1. The Load Balancer
2. The Service Mesh