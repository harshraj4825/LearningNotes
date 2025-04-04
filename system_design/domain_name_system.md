## Domain name system
A Domain Name System(DNS) translates a domain name such as www.example.com to an IP address.  

-Adreess book of all of internet.
-Translates "google.com" to 173.194.115.96
-Invented in 1983 by Paul Mokapetris (UC Irvine)
Without DNS, The internet & Network communications world stop.
![image](https://github.com/user-attachments/assets/16500ac4-becb-441c-b08c-f8b9dc0e4c74)

DNS is hierarchical, with a few authoritative servers at the top level. Your router or ISP provides information about 
which DNS server(S) to contant when doing lookup. Lower level DNS servers cache mappings, which could become stale due to DNS propagation 
deleys. DNS results can also be cached by browser or OS for a certain period of time, determined by the TTL.
- NS record (Name server) : Specifies the DNS servers for your domain/subdomain.
- MX record (main exchange): Specifies the mail servers for accepting messages.
- A record (address): Points a name to an IP address.
- CNAME (canonical): Points a name to another name or CNAME or an A record.

Services such as CloudFlare and Route 53 provide managed DNS services. Some DNS services can route traffic through various methods:
- Weighted round robin
  - Prevent traffic from going to servers under maintennce.
  - Balance between varying cluster sizes
  - A?B testing
- Latency-based
- Geolocation-based

#### Disadvantage(s): DNS
- Accessing a DNS server introduces a slight delay, although mitigated by caching described above.
- DNS server management could be complex and is generally managed by governments, ISPs, and Large companies.
- DNS services have recently come under DDos attach, preventing users from accessing websites such as Twitter without knowing Twitter's IP address(es).
