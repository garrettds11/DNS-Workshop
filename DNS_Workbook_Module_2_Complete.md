# Module 2: Domain Names

## 2.1 TLDs and ccTLDs

Top-Level Domains (TLDs) represent the highest level in the DNS hierarchy. They are divided into:
- Generic TLDs (gTLDs): `.com`, `.org`, `.net`
- Country-code TLDs (ccTLDs): `.us`, `.uk`, `.de`

ICANN is responsible for coordinating TLD management globally. Domain registries operate specific TLDs under ICANN contracts or oversight.

---

## 2.2 Domain Hierarchy

A domain name like `www.example.com` is hierarchical and read from right to left:
```
TLD → Domain → Subdomain
```

The Fully Qualified Domain Name (FQDN) ends with a dot indicating the root: `www.example.com.`

To trace DNS resolution:
```
dig +trace www.example.com
```

---

## 2.3 Registries vs Registrars

- **Registries** maintain TLD databases (e.g., Verisign for `.com`)
- **Registrars** are companies authorized to sell domain names (e.g., Namecheap, GoDaddy)

Registrars update the TLD's registry with nameserver information during domain registration.

---

## 2.4 ICANN Oversight

ICANN (Internet Corporation for Assigned Names and Numbers) manages:
- Global DNS coordination
- IP addressing policies
- Accreditation of registrars
- Delegation of TLDs to registries

---

## 2.5 WHOIS and RDAP

- **WHOIS** shows domain registration info: owner, registrar, creation/expiration dates.
- **RDAP** is a modern protocol that provides the same data in a structured, secure format.

Query examples:
```
whois example.com
https://rdap.org/domain/example.com
```

---

## 2.6 Internationalized Domain Names (IDNs)

IDNs allow domain names to use non-ASCII characters (e.g., `café.com`).

Encoded with **Punycode**:
```
café.com → xn--caf-dma.com
```

---

## 2.7 Domain Lifecycle

Domain lifecycle stages:
- **Active**
- **Expired**
- **Grace Period**
- **Redemption Period**
- **Pending Delete**
- **Available again**

Unrenewed domains eventually return to public registration.

---

## 2.8 Domain Transfer

Domain transfers move domain ownership between registrars using an **EPP/Auth code**.

Steps:
1. Unlock domain
2. Request Auth code
3. Submit to new registrar
4. Confirm transfer email

```
Get Auth Code → Submit to New Registrar → Confirm Email
```

Be aware of 60-day transfer lock after registration or transfer.
