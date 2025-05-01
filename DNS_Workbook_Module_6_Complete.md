# Module 6: Debugging DNS Issues

## 6.1 Cache Invalidation

DNS records are cached. To test changes or force fresh resolution, you must flush or bypass the cache.

### On clients:
- Windows: `ipconfig /flushdns`
- macOS: `sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder`
- Linux (systemd): `systemd-resolve --flush-caches`

---

## 6.2 Inspecting DNS Traffic

Use network analysis tools to capture and inspect DNS traffic.

- **tcpdump** (Linux/macOS):
```
sudo tcpdump -i any port 53
```

- **Wireshark**:
Apply filter: `dns`

---

## 6.3 Simulating Failures

To simulate DNS failures:
- Block outbound port 53
- Override `/etc/hosts`
- Misconfigure NS records
- Change TTLs to very short values for stress testing

---

## 6.4 Lame Delegation

Occurs when a domain is delegated to a nameserver that isn't authoritative for it.

Check:
```
dig example.com NS
dig @ns1.example.com example.com
```

If `ns1` doesn't respond authoritatively, it's a lame delegation.

---

## 6.5 DNSSEC Validation Errors

DNSSEC failures can result from:
- Expired signatures
- Missing DNSKEYs
- Incorrect trust chain

Tools:
```
dig +dnssec example.com
```

---

## 6.6 Root Cause Analysis

Steps to trace a DNS problem:
1. Verify if the problem is on the client or network
2. Try alternate resolvers (`1.1.1.1`, `8.8.8.8`)
3. Use `dig +trace` to walk the DNS chain
4. Compare behavior across multiple devices or networks

---

## 6.7 Graceful DNS Changes

To change DNS records safely:
- Lower TTL 1–2 days before a planned change
- Deploy changes
- Wait until old TTLs expire
- Raise TTL back

Use:
```
dig example.com ANY
```

to review current TTL values.

---

🛠️ Tools:
- `dig`, `host`, `nslookup`
- Wireshark
- DNSViz (https://dnsviz.net/)
- Zonemaster (https://zonemaster.net/)
