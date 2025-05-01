# Module 4: Types of DNS Records

## 4.1 A and AAAA Records

- **A Record** maps a domain to an IPv4 address.
- **AAAA Record** maps a domain to an IPv6 address.

```
dig example.com A
dig example.com AAAA
```

---

## 4.2 CNAME Records

- A **CNAME** (Canonical Name) record maps an alias to another domain name.
- It cannot coexist with other records for the same name.

```
dig www.example.com CNAME
```

---

## 4.3 TXT Records

- **TXT** records store arbitrary text.
- Common use cases: SPF, DKIM, site verification.

```
dig example.com TXT
```

---

## 4.4 SRV Records

- **SRV** (Service) records define service location and ports.
- Format: `_service._protocol.domain`

Example:
```
dig _sip._tcp.example.com SRV
```

---

## 4.5 PTR Records

- **PTR** (Pointer) records map IP addresses to domain names (reverse DNS).
- Used in logging and email validation.

Find reverse zone for IP:
```
dig -x 8.8.8.8
```

---

## 4.6 DNSSEC-Related Records

DNSSEC introduces new record types:
- **RRSIG** – digital signature for RRset
- **DNSKEY** – public key used in signatures
- **DS** – delegation signer (parent->child trust)
- **NSEC** / **NSEC3** – proof of non-existence

Examples:
```
dig example.com DNSKEY
dig example.com RRSIG
```

DNSSEC helps prevent spoofing by cryptographically validating DNS data.

---

Explore record types on:
- [Google Dig Tool](https://toolbox.googleapps.com/apps/dig/)
- `host`, `dig`, `nslookup`, `Resolve-DnsName`
