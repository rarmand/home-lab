### Check IP address

Input:
```
dig ferrari.com a
```

Full output:
```
; <<>> DiG 9.10.6 <<>> ferrari.com a
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 1915
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ferrari.com.                   IN      A

;; ANSWER SECTION:
ferrari.com.            60      IN      A       18.66.233.8
ferrari.com.            60      IN      A       18.66.233.83
ferrari.com.            60      IN      A       18.66.233.15
ferrari.com.            60      IN      A       18.66.233.34

;; Query time: 50 msec
;; SERVER: 192.168.1.10#53(192.168.1.10)
;; WHEN: Mon Sep 08 12:01:44 CEST 2025
;; MSG SIZE  rcvd: 104
```
____

### Reverse DNS lookup

Request type PTR - POINTER.

Input:

```
dig -x 192.168.1.10
```

Output:
```
...
Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 32709
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;10.1.168.192.in-addr.arpa.     IN      PTR
...
```

**NXDOMAIN** - Non-Existent Domain


Input:

```
dig -x 8.8.8.8
```

Output:
```
...
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34380
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   11646   IN      PTR dns.google.
...
```

### Check TXT from authoritative DNS server

Input:
```
dig @dns.google ferrari.com ns
```

Output:
```
; <<>> DiG 9.10.6 <<>> @dns.google ferrari.com ns
; (2 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16637
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;ferrari.com.                   IN      NS

;; ANSWER SECTION:
ferrari.com.            21600   IN      NS      margot.ns.cloudflare.com.
ferrari.com.            21600   IN      NS      zac.ns.cloudflare.com.

;; Query time: 47 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Mon Sep 08 13:12:09 CEST 2025
;; MSG SIZE  rcvd: 93
```

Here we got 2 authoritative servers.

Input:
```
dig @margot.ns.cloudflare.com ferrari.com txt
```

Output:
```
;; Truncated, retrying in TCP mode.

; <<>> DiG 9.10.6 <<>> @margot.ns.cloudflare.com ferrari.com txt
; (3 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22441
;; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65535
;; QUESTION SECTION:
;ferrari.com.                   IN      TXT

;; ANSWER SECTION:
ferrari.com.            60      IN      TXT     "Dynatrace-site-verification=dfd4e4b0-ae1d-481e-bf7d-73c3a2decc08__jutl5s9o8vjqqbtr51vkrb3a1v"
ferrari.com.            60      IN      TXT     "MS=ms46335663"
ferrari.com.            60      IN      TXT     "adobe-idp-site-verification=d57635812b33e27cd4b7e66b35e6c84d199273a0f68711b11f07c0ed2d2f8466"
ferrari.com.            60      IN      TXT     "atlassian-domain-verification=qYhiD0UawmdQRkkEg4BX4yV6SAvtFxW9WPRJFugFdH34f3thE0XmSdC8QZKBBYet"
ferrari.com.            60      IN      TXT     "cisco-ci-domain-verification=59cdefe6a28d1d96257b4f2e9e0f38e99e8f7ea9e934d4ce7ab341b0cf9cf595"
ferrari.com.            60      IN      TXT     "google-gws-recovery-domain-verification=44107073"
ferrari.com.            60      IN      TXT     "google-site-verification=EFb82ACVwqG-r-Uip6SN1iDIjIkNYd2_xlF_Er0XuMw"
ferrari.com.            60      IN      TXT     "google-site-verification=z6-plgFpnKIn2neng0Kpy-Ru1wtD_tPD8BijHHk8iQo"
ferrari.com.            60      IN      TXT     "onetrust-domain-verification=3999458cd7444a57931a3efd6533e3cb"
ferrari.com.            60      IN      TXT     "onetrust-domain-verification=fcadb43e27bb475b9948c6115b54a2a0"
ferrari.com.            60      IN      TXT     "ttnQxpGuDL80Nrfs5dBKVahZFgLsg9lzJi/MT12v2+CFSvTnff8N6I3f0IMWR3hQxB2jc2oHrixB3sUCkKkVgw=="
ferrari.com.            60      IN      TXT     "v=spf1 mx a:ferrari.it a:mail1.ferrari.it include:spf.protection.outlook.com ip4:141.206.158.132 ip4:141.206.158.133 ip4:193.42.138.0/24 ip4:91.192.40.0/22 ip4:81.144.241.76/32 ip4:77.223.1.130/32 ip4:216.146.32.160/27 ip4:34.241.108" ".177/32 ip4:46.37.16.7/32 -all"
ferrari.com.            60      IN      TXT     "webexdomainverification.=72b8b7dd-8ccd-422b-972f-d3599bdd032e"

;; Query time: 20 msec
;; SERVER: 108.162.194.167#53(108.162.194.167)
;; WHEN: Mon Sep 08 13:12:29 CEST 2025
;; MSG SIZE  rcvd: 1312
```

The flags are interesting. We are getting:
- qr - query,
- aa - authoritative answer,
- rd - recursion desired,

and no _ra_ flag.

Also, we are getting ANSWERS: 13.

The message is too large for UDP single packet (512 B by default), so the message is truncated and next, the process looks like it is repeated in TCP mode. We do not get a TR flag - _truncated_.