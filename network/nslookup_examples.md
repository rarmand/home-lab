Used Bash on macOS.

### Check IPv4

Request:
```
nslookup wikipedia.org
```

Response from macOS's terminal:

```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
Name:   wikipedia.org
Address: 185.15.59.224
```

Response from Windows's cmd:

```
Server:  UnKnown
Address:  192.168.1.10

Non-authoritative answer:
Name:    wikipedia.org
Addresses:  2a02:ec80:300:ed1a::1
          185.15.59.224
```

First 2 lines: private IP address from local net. Not public.

In the first response we see added __#53__ what means used UDP port 53.

With Windows CMD ...

**Non-authoritative answer:**

means that the responding DNS server is not the autoritative server for the domain. The response comes from a cached copy of the DNS data. The data is usually stored by an intermediate server (ISP's DNS server).

To get an authoritative answer, we can query the authoritative DNS server directly.

The last 2 lines show the correct reponse:

- name of the requested domain
- IP address 

__Fun fact__: Windows's CMD shows also IPv6.


To request the authoritative server, first we need to request for the NS records of the domain:

```
nslookup -type=NS wikipedia.ord
```

The response
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
wikipedia.org   nameserver = ns1.wikimedia.org.
wikipedia.org   nameserver = ns2.wikimedia.org.
wikipedia.org   nameserver = ns0.wikimedia.org.

Authoritative answers can be found from:
```

Next, we request the server directly:

Request:
```
nslookup wikipedia.org ns1.wikimedia.org
```

Response:
```
Server:         ns1.wikimedia.org
Address:        208.80.153.231#53

Name:   wikipedia.org
Address: 185.15.59.224
```