#System Design

##Basic Steps

1) Clarify and agree on the scope of the system
* Use cases (description of sequences of events that, taken together, lead to a system doing something useful)
	* Who is going to use it?
	* How are they going to use it?
* Constraints 
	* Mainly identify traffic and data handling constraints at scale.
	* Scale of the system such as requests per second, requests types, data written per second, data read per second)
	* Special system requirements such as multi-threading, read or write oriented.
	
2) High level architecture design (Abstract design)
* Sketch the important components and connections between them, but don't go into some details.
	* Application service layer (serves the requests) -* List different services required.
   	* Data Storage layer
   	* eg. Usually a scalable system includes webserver (load balancer), service (service partition), database (master/slave database cluster) and caching systems.

3) Component Design
* Component + specific APIs required for each of them.
* Object oriented design for functionalities.
	* Map features to modules: One scenario for one module.
	*Consider the relationships among modules: 
		* Certain functions must have unique instance (Singletons)
		* Core object can be made up of many other objects (composition).
		* One object is another object (inheritance)
* Database schema design.

4) Understanding Bottlenecks
* Perhaps your system needs a load balancer and many machines behind it to handle the user requests. * Or maybe the data is so huge that you need to distribute your database on multiple machines. What are some of the downsides that occur from doing that? 
* Is the database too slow and does it need some in-memory caching?	

5) Scaling your abstract design
* Vertical scaling
	* You scale by adding more power (CPU, RAM) to your existing machine.
* Horizontal scaling
	* You scale by adding more machines into your pool of resources. 
* Caching
	* Load balancing helps you scale horizontally across an ever-increasing number of servers, but caching will enable you to make vastly better use of the resources you already have, as well as making otherwise unattainable product requirements feasible. 	
	* In-memory caches like Memcached or Redis are good choices. Please never do file-based caching, it makes cloning and auto-scaling of your servers just a pain. 
	* eg. Precalculating results (e.g. the number of visits from each referring domain for the previous day), 
	* eg. Pre-generating expensive indexes (e.g. suggested stories based on a user's click history)
	* eg. Storing copies of frequently accessed data in a faster backend (e.g. Memcache instead of PostgreSQL.
* Load balancing
	* Public servers of a scalable web service are hidden behind a load balancer.  This load balancer evenly distributes load (requests from your users) onto your group/cluster of  application servers.
	* Types: Smart client (hard to get it perfect), Hardware load balancers ($$$ but reliable), Software load balancers (hybrid - works for most systems)

<p align="center">
  <img src="http://lethain.com/static/blog/intro_arch/load_balance.png" alt="Load Balancing"/>
</p>

* Database replication
	* Database replication is the frequent electronic copying data from a database in one computer or server to a database in another so that all users share the same level of information. The result is a distributed database in which users can access data relevant to their tasks without interfering with the work of others. The implementation of database replication for the purpose of eliminating data ambiguity or inconsistency among users is known as normalization.
* Database partitioning
	* Partitioning of relational data usually refers to decomposing your tables either row-wise (horizontally) or column-wise (vertically).

##Key topics for designing a system

1) Concurrency 
* Do you understand threads, deadlock, and starvation? Do you know how to parallelize algorithms? Do you understand consistency and coherence?

2) Networking
* Do you roughly understand IPC and TCP/IP? Do you know the difference between throughput and latency, and when each is the relevant factor?

3) Abstraction
* You should understand the systems you’re building upon. Do you know roughly how an OS, file system, and database work? Do you know about the various levels of caching in a modern OS?

4) Real-World Performance
* You should be familiar with the speed of everything your computer can do, including the relative performance of RAM, disk, SSD and your network.

5) Estimation
* Estimation, especially in the form of a back-of-the-envelope calculation, is important because it helps you narrow down the list of possible solutions to only the ones that are feasible. Then you have only a few prototypes or micro-benchmarks to write.	

6) Availability & Reliability
*  Are you thinking about how things can fail, especially in a distributed environment? Do know how to design a system to cope with network failures? Do you understand durability?


##Web UI System design topics:
* Security (CORS)
* Offline support/Progressive enhancement?
* Accessibility
* Internationalization
* Responsive design
* Browser compatibility

**Links**

[How to rock a systems design interview](http://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)

[System Design Interviewing](http://www.hiredintech.com/system-design/)

[Scalability for Dummies](http://www.lecloud.net/tagged/scalability)

[Introduction to Architecting Systems for Scale](http://lethain.com/introduction-to-architecting-systems-for-scale/)

[Scalable System Design Patterns](http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)

[Scalable Web Architecture and Distributed Systems](http://www.aosabook.org/en/distsys.html)

[What is the best way to design a web site to be highly scalable?](http://programmers.stackexchange.com/a/108679/62739)