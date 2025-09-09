### ISP - Internet Service Provider 

At first, we get any information about domains and IP addresses "from our ISP" - ISP's DNS resolver.

The default DNS server - DNS resolver, provided by ISP - keeps copies of information from other higher-authority DNS servers.

Such DNS servers are like a phonebook of the web - we have contact numbers to specific domains. Such a DNS Resolver allows or disallows us to contact with specific addresses.

"Some DNS servers cache frequently accessed domains to speed up the resolution process. Others employ encryption and filtering to block malicious websites and prevent cyber threats."

> https://cyble.com/knowledge-hub/best-dns-servers-for-security/

### DNS infrastructure

DNS infrastructure primarily involves two key types of servers: recursive and authoritative. Recursive DNS servers serve as intermediaries between users and the Internet’s vast DNS database.

When a user types a website address, the recursive server takes the request and searches through the DNS hierarchy to find the correct IP address, caching results for faster responses in the future. Authoritative DNS servers, on the other hand, hold the definitive records for specific domains.

### Interesting servers

1. Cloudflare DNS 

**Cloudflare DNS (1.1.1.1)** is known for its high speed and privacy-centric approach. It doesn’t log user data and offers strong security against cyber threats. 

Pros: Fast response time, strong encryption, zero user tracking.
Cons: Limited filtering and parental control options.
Best for: Users prioritizing speed and privacy.

2. Google DNS Servers 

**Google Public DNS (8.8.8.8 and 8.8.4.4)** is one of the most widely used and reliable DNS options. 

Pros: High uptime, faster domain resolution, strong security against DNS attacks. 
Cons: Google collects some user data.
Best for: General users needing reliability and speed.

> https://www.lh.pl/pomoc/iana-co-to-jest/

___

**IANA** - Internet Assigned Numbers Authority 
An organization responsible for globally coordinating key elements of the Internet’s infrastructure. Its main roles are:

- **IP address allocation** - IANA manages the central pool of IP addresses and delegates large address blocks to five Regional Internet Registries (RIRs), who then distribute them to Internet service providers and organizations.

- **DNS root zone management** - IANA maintains the root zone of the Domain Name System (DNS), which is the highest level of the DNS hierarchy and contains information about top-level domains (TLDs) like .com, .org, and .net.

- **Protocol parameters** - IANA coordinates the assignment of unique numbers and names used in Internet protocols—such as port numbers and other technical parameters—to ensure consistent and interoperable communication worldwide.

IANA performs these functions as an affiliate of ICANN, which took over responsibility from earlier government and academic administration. Its activities are critical for the stability, interoperability, and security of the global Internet
___

1. Zarządzanie adresami IP: IANA odpowiada za alokację bloków adresów IP (zarówno IPv4, jak i IPv6) do regionalnych rejestrów internetowych (RIR), które następnie przydzielają te adresy indywidualnym użytkownikom i organizacjom.

2. Zarządzanie DNS: IANA zarządza systemem nazw domen (DNS), w tym domenami najwyższego poziomu (TLD). Oznacza to, że IANA nadzoruje struktury DNS i zapewnia, że domeny są odpowiednio przydzielane i zarządzane.

3. Zarządzanie numerami i parametrami protokołów internetowych: IANA zajmuje się również zarządzaniem numerami portów, parametrami protokołów oraz innymi technicznymi identyfikatorami używanymi w sieciach komputerowych.

IANA działa jako część ICANN (Internet Corporation for Assigned Names and Numbers), organizacji non-profit, która nadzoruje i koordynuje wiele kluczowych funkcji internetu na poziomie globalnym.
___