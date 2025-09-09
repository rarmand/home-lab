### Check IP address 

Input:
```
nslookup memrise.com
```

Output:
```
...
Non-authoritative answer:
Name:   memrise.com
Address: 34.239.199.159
Name:   memrise.com
Address: 34.196.92.160
Name:   memrise.com
Address: 34.228.137.72
Name:   memrise.com
Address: 44.206.207.74
Name:   memrise.com
Address: 34.195.148.202
Name:   memrise.com
Address: 54.146.243.148
```

Input:
```
ping 34.239.199.159
```

Output:
```
PING 34.239.199.159 (34.239.199.159): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
Request timeout for icmp_seq 3
...
```

**56 data bytes** - a standard size of data packet sent in one ICMP.

**Requested timeout for icmp_seq** - ICMP Echo Request packet is sent, but we get no response (ICMP Echo Reply) in specific time limit from the target: from a host or server.

<br></br>
After checking all IP addresses, it looks like all IPs are not responding. It is interesting.
___