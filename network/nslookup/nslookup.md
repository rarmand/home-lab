#### nslookup

> https://www.nslookup.io/
> https://www.nslookup.io/learning/

A diagnostic tool to request Domain Name System servers about more details of DNS records (hostnames or IP addresses).  

<br/><br/>
Operates at the OSI's **Application layer 7**.

Uses UDP port 53.
Uses TCP port 53 as a default fallback.

<br/><br/>
Available record types: 52.

The most common:

- A - hostname's IPv4 address
- AAAA - hostname's IPv6 address
- CNAME - Canonical Name
- MX - mail exchange if assigned to the domain
- NS - name server
- TXT - human-readable text
- SOA - start of authority

<br/><br/>
Usable for:
- DNS diagnostics
- Tracerouting
- Configuration verification
- Connection troubleshooting

Przykład zapytania:

```
nslookup -query=A wikipedia.org
```

```
nslookup -type=AAAA wikipedia.org
```