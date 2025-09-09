### Check not responding IP address 

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


### Check responding IP address


Input:
```
ping filharmoniakrakow.pl
```

Output:
```
PING filharmoniakrakow.pl (46.242.202.251): 56 data bytes
64 bytes from 46.242.202.251: icmp_seq=0 ttl=49 time=35.206 ms
64 bytes from 46.242.202.251: icmp_seq=1 ttl=49 time=54.633 ms
64 bytes from 46.242.202.251: icmp_seq=2 ttl=49 time=39.348 ms
...
--- filharmoniakrakow.pl ping statistics ---
8 packets transmitted, 8 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 35.206/42.016/54.633/5.424 ms
```

Here, we get a correct response with ICMP Echo Reply.

We get info:
- packets transmitted - 8
- packets received - 8
- packet loss - 0.0%
- round-trip min - 35.206 ms
- round-trip average - 42.016 ms
- round-trip max - 54.633 ms
- round-trip stddev - 5.424 ms

Nice and easy.