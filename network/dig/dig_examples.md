### Check IP address

Input:
```
dig ferrari.com a
```

Output:
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