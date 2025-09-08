### Check IP address

Input:
```
nslookup wikipedia.org
```

Output from macOS terminal:

```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
Name:   wikipedia.org
Address: 185.15.59.224
```

Output from Windows CMD:

```
Server:  UnKnown
Address:  192.168.1.10

Non-authoritative answer:
Name:    wikipedia.org
Addresses:  2a02:ec80:300:ed1a::1
          185.15.59.224
```
____
<br></br>
First 2 lines: a private IP address from  a local net. Not public. In this case we get only IPv4 address.

In the first output we see an added __#53__, what means a used UDP port 53, because the request is sent from our IP. ???

<br></br>
The output from Windows CMD differs from Linux one. This is likely due to differences in the way the **nslookup** tool is implemented and its default configuration in each operating system.

The interactive version of **nslookup** should present more information about the sender.
____
<br></br>
**Non-authoritative answer:**

means that the responding DNS server is not the autoritative server for the domain. The response comes from a cached copy of the DNS data. The data is usually stored by an intermediate server (ISP's DNS server).

To get an authoritative answer, we can query the authoritative DNS server directly.
___

The last 2 lines show the correct reponse:

- a name of the requested domain
- an IP address 

__Fun fact__: Windows CMD presents both IPv6 and IPv4 addresses. This suggests that the CMD version of the tool is designed to request and display more comprehensive DNS information by default.
____
<br></br>
To request the authoritative server, first we need to request for the NS records of the domain:

Input:
```
nslookup -type=NS wikipedia.ord
```

Output:
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

Input:
```
nslookup wikipedia.org ns1.wikimedia.org
```

Output:
```
Server:         ns1.wikimedia.org
Address:        208.80.153.231#53

Name:   wikipedia.org
Address: 185.15.59.224
```
___
### Check a specific type of information about a domain

Here, we use **-query=[TYPE]**.

In this example, we request for an info about an IPv6 address - type **AAAA**.

Input:
```
nslookup -query=AAAA wikipedia.org
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
wikipedia.org   has AAAA address 2a02:ec80:300:ed1a::1

Authoritative answers can be found from:

```

The response is correct, still from a non-authoritative server.

The IPv6 address matches the one provided by the CMD nslookup.
___

### Check MX of a domain

It is possible to check if the hostname uses any server to manage mails. Here we use **MX type - mail exchange**. 

This record type exists in the DNS to support another protocol. It is critical to the delivery of email via the Simple Mail Transfer Protocol (SMTP).

> https://www.nslookup.io/learning/dns-record-types/mx/

Input:
```
nslookup -query=MX wikipedia.org
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
wikipedia.org   mail exchanger = 10 mx-in2001.wikimedia.org.
wikipedia.org   mail exchanger = 10 mx-in1001.wikimedia.org.

Authoritative answers can be found from:

```

The output presents:

- hostname
- type of info 
- **preference**: a 16-bit unsigned integer value. Lower values indicate higher preference. It is legal to have a preference value zero. This indicates the highest possible preference.
- **mail exchange**: the fully qualified DNS name of a mail exchange for the domain.

<br></br>
**The preference is interesting.**
The MX preference field allows the mail administrator for the domain to control the order in which mail servers are used by SMTP clients. 

SMTP clients are required to contact the lowest preference mail server first. SMTP clients are only permitted to use higher preference mail servers if all the mail servers with lower preference are unreachable or return error.

If two MX records have the same preference value, the SMTP client is required to randomize its requests to load balance equally among all mail servers of the same preference value.

As the value increases, preference for the mail server in that particular MX record decreases.

In this example, the sender has a 50% chance to use a mail exchanger no. 1 and a 50% chance to use a mail exchanger no. 2.
___

### Check NS of a domain

**NS - Name Server**

The answer usually comes from the DNS server provided by an ISP.

Input:
```
nslookup -query=NS wikipedia.org
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
wikipedia.org   nameserver = ns0.wikimedia.org.
wikipedia.org   nameserver = ns1.wikimedia.org.
wikipedia.org   nameserver = ns2.wikimedia.org.

Authoritative answers can be found from:
wikipedia.org   nameserver = ns1.wikimedia.org.
wikipedia.org   nameserver = ns2.wikimedia.org.
wikipedia.org   nameserver = ns0.wikimedia.org.
```
____

### Check CNAME of a domain

Input:
```
nslookup -query=CNAME wikipedia.org
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
*** Can't find wikipedia.org: No answer

Authoritative answers can be found from:
wikipedia.org
        origin = ns0.wikimedia.org
        mail addr = hostmaster.wikimedia.org
        serial = 2025080821
        refresh = 43200
        retry = 7200
        expire = 1209600
        minimum = 3600

```

Input:
```
nslookup -query=CNAME 8.8.8.8
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
8.8.8.8.in-addr.arpa    name = dns.google.

Authoritative answers can be found from:

```
____

### Request to another DNS Server

Here, we can use:
- Cloudflare DNS - 1.1.1.1
- Google Public DNS - 8.8.8.8 or 8.8.4.4

#### Google Public DNS

Input:
```
nslookup -query=CNAME 8.8.8.8
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
8.8.8.8.in-addr.arpa    name = dns.google.

Authoritative answers can be found from:

```

Input:
```
nslookup dns.google
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
Name:   dns.google
Address: 8.8.4.4
Name:   dns.google
Address: 8.8.8.8

```

Input:
```
nslookup -query=NS wikipedia.org 8.8.4.4
```

Output:
```
Server:         8.8.4.4
Address:        8.8.4.4#53

Non-authoritative answer:
wikipedia.org   nameserver = ns0.wikimedia.org.
wikipedia.org   nameserver = ns1.wikimedia.org.
wikipedia.org   nameserver = ns2.wikimedia.org.

Authoritative answers can be found from:

```

#### Cloudflare

Input:
```
nslookup 1.1.1.1
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
1.1.1.1.in-addr.arpa    name = one.one.one.one.

Authoritative answers can be found from:

```

Input:
```
nslookup -query=cname one.one.one.one
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
*** Can't find one.one.one.one: No answer

Authoritative answers can be found from:
one.one.one
        origin = dorthy.ns.cloudflare.com
        mail addr = dns.cloudflare.com
        serial = 2382211228
        refresh = 10000
        retry = 2400
        expire = 604800
        minimum = 1800

```

What does it mean?
1. No answer is found.
2. Next - Authoritative SOA Record Details - Start of Authority record, which contains administrative and technical details about the domain:

	• **origin** - the primary authoritative nameserver for the zone.

	• **mail addr** - the administrator’s email address (SOA stores `@` as a dot, i.e., `dns@cloudflare.com`).

	• **serial** - version number for the DNS zone file; increases with each change.

	• **refresh** - time interval (in seconds) after which secondary DNS servers should check for updates.

	• **retry** - time interval for how long a secondary server should wait before retrying updates.

	• **expire** - how long a secondary can use zone data without successful updates.

	• **minimum** - default TTL (time to live) for records in the zone.
____

### Request for a domain with an IP address

Input:
```
nslookup 8.8.8.8
```

Output:
```
Server:         192.168.1.10
Address:        192.168.1.10#53

Non-authoritative answer:
8.8.8.8.in-addr.arpa    name = dns.google.

Authoritative answers can be found from:

```