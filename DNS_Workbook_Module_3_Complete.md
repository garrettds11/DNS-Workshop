# Module 3: Operational DNS

## 3.1 Recursive Queries

Recursive DNS servers resolve queries on behalf of clients. When a client asks for a domain, the recursive server performs all necessary steps to get the answer from the authoritative server.

Try:
```
dig +trace openai.com
```

---

## 3.2 Glue Records

Glue records prevent circular dependencies in delegation. When a nameserver is within the domain it serves, a glue record (A or AAAA) is required to resolve the IP of the NS.

Check:
```
dig com NS
dig example.com NS +additional
```

---

## 3.3 DNS Caching and TTL

DNS responses are cached to improve performance. The Time To Live (TTL) determines how long a response can be cached.

Check TTL:
```
dig example.com
```

---

## 3.4 Negative Caching

If a domain does not exist (NXDOMAIN), the response is also cached. The SOA record's minimum field influences this.

Try:
```
dig nonexistent.example.com
```

---

## 3.5 DNS Protocol

DNS uses UDP by default on port 53 and switches to TCP for larger messages or zone transfers. The DNS message format includes:
- Header
- Question
- Answer
- Authority
- Additional

Explore DNS packets using:
- `tcpdump -i any port 53`
- Wireshark with a DNS filter

---

## 3.6 EDNS (Extension Mechanisms for DNS)

EDNS extends DNS capabilities, allowing larger message sizes and DNSSEC support.

Check:
```
dig +edns=0 example.com
```

---

## 3.7 Transport Protocols

DNS primarily uses:
- **UDP** (default)
- **TCP** (fallback)
- **DNS over HTTPS (DoH)** and **DNS over TLS (DoT)** (for privacy)

Modern tools and resolvers support encrypted DNS like:
- Cloudflare's DoH: `https://cloudflare-dns.com/dns-query`

---

## 3.8 Public Resolvers

Well-known recursive resolvers:
- Google: `8.8.8.8`
- Cloudflare: `1.1.1.1`
- Quad9: `9.9.9.9`

Test:
```
dig @1.1.1.1 example.com
```

---

## 3.9 Dynamic DNS (DDNS)

DDNS allows automatic updates of DNS records, commonly used in home networks and with VPNs.

Example:
- A home router updates `myhome.dyndns.org` when its IP changes.

---

## 3.10 Dynamic DNS Responses

DNS responses can vary based on:
- Geographic location
- Load balancing needs
- Device type

This is known as **split-horizon DNS** or **geo-DNS**.

Check:
```
dig example.com @8.8.8.8
dig example.com @1.1.1.1
```

Compare answers based on location and resolver.
