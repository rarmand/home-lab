### What is it?

**Traceroute** - network diagnostic tool.

A command-line tool used in Linux or other operating systems to track the path that data takes from your computer to a specified destination, such as a website.

> https://www.geeksforgeeks.org/linux-unix/traceroute-command-in-linux-with-examples/

The result shows each "hop" that the data packet makes along its journey.

This includes different servers and devices it passes through (e.g. WI-FI) and how long each step takes.


- the number of hops (routers)
- the round-time trip (RTT) for each hop
____

### Basic syntax

```
traceroute [options] destination_address
```

### The difference between _ping_ and _traceroute_

The main difference between ping and traceroute is:

- **Ping** checks if a server is reachable and shows how long it takes to send and receive data.
- **Traceroute** shows the exact path data takes to reach the server, listing each stop (router) along the way and how long each stop takes.
