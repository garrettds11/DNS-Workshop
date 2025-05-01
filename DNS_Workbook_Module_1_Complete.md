# Module 1: DNS from First Principles

## 1.1 DNS as a Database

The Domain Name System (DNS) operates as a globally distributed, hierarchical database that maps domain names to various types of data. DNS records are stored as resource records (RRs), consisting of fields like name, type, class, TTL, and data. Each entry is cached to improve resolution speed and minimize redundant lookups.

DNS replaced the early HOSTS.TXT file with a scalable, decentralized system. Every interaction on the internet — browsing, email, VPN — depends on DNS resolution.

```
example.com. 86400 IN A 93.184.216.34
```

This record maps example.com to the IPv4 address 93.184.216.34 for a TTL of 86400 seconds (1 day).

### 💻 Lab 1.1 – Querying DNS Records

**Objective**: Use command-line tools to query DNS records.

```
dig example.com A
dig example.com MX
dig example.com TXT
nslookup -type=MX gmail.com
Resolve-DnsName example.com
```

Compare TTLs, record types, and whether the response is authoritative.

**Challenge**: Investigate a domain and list all record types it uses, along with their TTLs.

---

## 1.2 DNS Structure

DNS is organized hierarchically. The root (.) is at the top, followed by TLDs (.com, .net), then second-level domains (example.com), and subdomains (www.example.com).

```
dig +trace www.example.com
```

This command shows how resolution walks from the root to the authoritative server.

---

## 1.3 Zone Delegation

Authority over DNS zones is delegated from parent to child domains. TLDs delegate to registrars who delegate to domain owners.

```
dig NS example.com +trace
```

Use this to follow delegation down the DNS hierarchy.

---

## 1.4 The Root Zone

The root zone contains pointers to all TLD servers and is operated by organizations under the oversight of IANA and ICANN.

```
dig . NS
```

This lists the root servers responsible for starting DNS resolution.

---

## 1.5 Authoritative DNS Servers

An authoritative server holds original zone records and responds to queries with definitive answers. It contrasts with recursive resolvers, which fetch data by querying multiple servers.

```
dig @ns1.example.com example.com A
```

This shows how to directly query an authoritative server.

---

## 1.6 Zone Transfer

Zone transfers (AXFR, IXFR) replicate zone data between primary and secondary authoritative servers.

```
dig @ns1.example.com example.com AXFR
```

Note: Most servers disable AXFR to prevent data leaks.

---

## 1.7 Using Dig and Nslookup

These tools are used to inspect DNS behavior and troubleshoot resolution issues.

```
dig +short google.com
dig +trace gmail.com
nslookup -type=TXT openai.com
Resolve-DnsName github.com -Type A
```

Explore differences in output, especially across authoritative vs recursive answers.
