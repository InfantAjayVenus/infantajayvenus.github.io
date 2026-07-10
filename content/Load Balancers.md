---
tags:
  - hld
---
A Load Balancer is an infrastructural component that takes in a requests and routes it to one of a fleet of servers that handles that specific type of request and it does so in a way as to distribute the traffic equally across all the servers. This ensures that no one server is being overloaded with requests or is idle.

### Distribution Algorithms
To achieve equal distribution of traffic, load balancers can be configured to follow one of several algorithms. Those algorithms are as follows,

#### Round Robin
Here every request is sequentially routed to the next server in queue. For instance, given there are servers A, B and C, the first request is handed over to Server A, the second is handed over to Server B, the third is routed to Server C, the fourth again to Server A and so on. This is a very simple technique and is effective when all the servers are configured with the same physical specification (CPU Cores, Memory, Network Bandwidth etc.,)

#### Weighted Round Robin
This is very similar to simple Round Robin, except that it does not treat all servers equally. A weight is added to each server based on their physical configuration and the request routing is rounded based on the weight.
For instance, say we have 2 servers, where Server A has 8 CPU Cores and Server B with 4 CPU cores. We weight Server A as 2 and Server B as 1. Now when the requests come in, the first two requests are routed to Server A and the third request is routed to Server B.

#### Least Connections
This is where an incoming request is routed to the server that has the least active connections at that moment. This is very effective in cases where some requests may take more time to process than others.

#### IP Hashing
This is a technique where the source IP address of the incoming request is passed through an Hashing function that maps the request to a specific server. This leads to a case where a given user is always routed to the same server. Here distribution can be achieved by modifying the hash function.

### Health Checks, Fail overs and Recovery
Load Balancers fire health check requests or heart beat requests to all the server in the fleet periodically (say 5s), when a server doesn't respond to a health check request, based on the tolerance policy (for instance, 3 consecutive health check failures) the load balancer marks the server as failed and removes it from the queue and distributes traffic across the remaining active servers. This prevents specific set of requests from failing.
To recover the failed servers back into queue load balancers follow two techniques,
1. Active Probing: Despite the health check failing, the load balancer keeps pinging the health check endpoint, once the server starts responding successfully enough to satisfy a recovery policy, that server is added back to the fleet. This technique helps catch abrupt crashes and completely avoids a request failures.
2. Passive Monitoring: The load balancer passively monitors the real time traffic and it's failure rates to a certain server an use that decide if the server is up or not. This technique catches subtle performance drops that simple pings couldn't detect, although at the cost of failed requests.

### Types of Load Balancers
Load balancers can look into the information in a request to help decide on how to route that request. Based on what kind of information the load balancer looks into, it can be classified as follows,
1. *Layer 4 Load Balancer / Network Load Balancer(NLB)*: This type of load balancers look into the TCP headers like the PORT and use that to route the traffic. This is extremely efficient and fast. This is useful when one or more servers are handling the same type of request with the same protocol (say FTP).
2. *Layer 7 Load Balancer / Application Load Balancer(ALB)*: This type of load balancer look into the application level information like URL, Cookies etc., These type of load balancers can be used to manage complex routing policies, for instance, routing authenticated users to a specific high bandwidth servers while guest users to low-bandwidth servers. This is comparatively slower than NLB.