# Module 5: Email and DNS

## 5.1 MX Records

- **MX (Mail Exchange)** records define the mail servers responsible for accepting email messages.
- Multiple MX records can be prioritized using the "preference" value (lower is higher priority).

Example:
```
dig gmail.com MX
```

---

## 5.2 SPF (Sender Policy Framework)

- **SPF** is a TXT record that specifies which mail servers are allowed to send email for a domain.
- Helps reduce spam and phishing.

Example:
```
dig example.com TXT
```

Look for: `"v=spf1 include:... ~all"`

---

## 5.3 DKIM (DomainKeys Identified Mail)

- **DKIM** adds a digital signature to email headers using a public key published in DNS.

Check for DKIM record:
```
dig default._domainkey.example.com TXT
```

---

## 5.4 DMARC (Domain-based Message Authentication, Reporting & Conformance)

- **DMARC** builds on SPF and DKIM to define how mail servers should handle failures.

Check:
```
dig _dmarc.example.com TXT
```

Common policy values:
- `p=none`
- `p=quarantine`
- `p=reject`

---

## 5.5 DANE (DNS-based Authentication of Named Entities)

- **DANE** uses DNSSEC to bind X.509 certificates (used in TLS) to domain names.
- Implemented via TLSA records.

Example:
```
dig _25._tcp.mail.example.com TLSA
```

---

## 5.6 MTA-STS (Mail Transfer Agent Strict Transport Security)

- **MTA-STS** enforces TLS for email delivery using HTTPS-hosted policy files and a DNS TXT record.

Check:
```
dig _mta-sts.example.com TXT
```

---

## 5.7 BIMI (Brand Indicators for Message Identification)

- **BIMI** displays brand logos in supported inboxes.
- Requires a DNS TXT record and valid DMARC policy.

Check:
```
dig default._bimi.example.com TXT
```

---

🛠️ Tools:
- [MXToolbox](https://mxtoolbox.com/)
- `dig`, `nslookup`, `host`
- Online SPF/DKIM/DMARC checkers
