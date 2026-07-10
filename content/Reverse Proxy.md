---
tags:
  - hld
  - core
---
Reverse Proxy sits in front of the application server, and routes the request to one or more applications deployed across one or more servers.

**Benefits**:
1. *Security*: The network of the application servers are hidden from the outside world.
2. *Performance*: A Reverse proxy can be configured to handle SSL Termination, compression and caching which can take the load off of the application servers.
3. *Improved Availability*: When a request has to be served with a long streaming response, the application server can hand over the response to the reverse proxy as a single large response which it then responds to the user at a rate suitable to the user. This technique is called `Spoon Feeding`. This allows the application server's resources to be freed early.