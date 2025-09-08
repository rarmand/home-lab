**DIG** - domain information groper

It is said that **dig** tool is more flexible and more often used by specialists to dig into the Web.

Interesting thing:
> https://toolbox.googleapps.com/apps/dig
> https://www.ibm.com/docs/pl/aix/7.1.0?topic=d-dig-command
> https://www.scaleway.com/en/docs/domains-and-dns/how-to/test-dns-zones-with-dig/

Regular query:

```
dig @server name type
```

- **server** - the name or IP address of the name server to query. This can be an IPv4 address in dotted-decimal notation or an IPv6 address in colon-delimited notation. When the supplied server argument is a hostname, the dig command resolves that name before querying that name server. If no server argument is provided, the dig command consults the /etc/resolv.conf file and queries the name servers listed there. The reply from the name server that responds is displayed.

- **name** - the name of the resource record that is to be looked up.

- **type** - indicates what type of query is required — ANY, A, MX, SIG, and so on. The type argument value can be any valid query type. If no type argument is supplied, the dig command performs a lookup for an A record. 


The output:
```
; <<>> DiG 9.10.6 <<>> -x 192.168.1.10
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 32709
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;10.1.168.192.in-addr.arpa.     IN      PTR

;; Query time: 27 msec
;; SERVER: 192.168.1.10#53(192.168.1.10)
;; WHEN: Mon Sep 08 12:43:10 CEST 2025
;; MSG SIZE  rcvd: 54
```

What do we have here?

-  ->>HEADER<<- **opcode**: QUERY - the type of DNS operation (usually QUERY for standard queries).

- **status**: NXDOMAIN - response status (NOERROR, NXDOMAIN, SERVFAIL).

- **id**: 32709 - query identifier to match requests and responses.

- **flags** - control flags indicating query and response properties, including:

    -   `QR`: Query/Response flag (0 = query, 1 = response).

	-	`AA`: Authoritative Answer (response from authoritative server).

	-	`TC`: Truncated response (when UDP packet is too large).

	-	`RD`: Recursion Desired (client requests recursive query).

	-	`RA`: Recursion Available (server supports recursive queries).

	-	`AD`: Authenticated Data (valid DNSSEC signature).

	-	`CD`: Checking Disabled (client requests disabling DNSSEC validation).

- Counts of records in sections: `QUERY`, `ANSWER`, `AUTHORITY`, `ADDITIONAL`.

- **QUESTION SECTION** - the domain name and query type requested.

- **ANSWER SECTION** - resource records that answer the query.

- **AUTHORITY SECTION** - nameservers authoritative for the zone (often show delegation information).

- **ADDITIONAL SECTION** - extra information aiding the resolution (e.g. IP addresses of name servers).

- **Query time** - time taken to receive the response.

- **SERVER** - the DNS server that answered.

- **WHEN** - timestamp of the query execution.

- **MSG SIZE** - size of the DNS message received.
<br></br>

> https://www.linux.com/training-tutorials/check-your-dns-records-dig/

____

Additional tools:

 - **-x** - used to make a reverse DNS query.

 - **-f** - reads queries from a file and returns the results.

 - **-c** - determines how many times the specified query will be executed.

 - **-p** - specifies the port used when making DNS queries.

 - **-y** - used with the HMAC-MD5 key and password to authenticate DNS queries.