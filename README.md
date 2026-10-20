# IT Security Tools Reference

Field manuals and quick-reference guides for security and OSINT tools.
Built from active lab work on Kali Linux.

---

## Nmap — Network Scanner

**Purpose:** Host discovery, port scanning, service/version detection, OS fingerprinting

### Core Commands

| Command | What It Does |
|---------|-------------|
| `nmap 192.168.1.1` | Basic scan — top 1000 ports |
| `nmap -sV 192.168.1.1` | Service/version detection |
| `nmap -O 192.168.1.1` | OS fingerprinting |
| `nmap -A 192.168.1.1` | Aggressive scan (OS + version + scripts + traceroute) |
| `nmap -p 22,80,443 192.168.1.1` | Scan specific ports |
| `nmap -p- 192.168.1.1` | Scan all 65535 ports |
| `nmap -sS 192.168.1.1` | SYN scan (stealth) — requires root |
| `nmap -sU 192.168.1.1` | UDP scan |
| `nmap -sn 192.168.1.0/24` | Ping sweep — discover live hosts |
| `nmap -oN output.txt 192.168.1.1` | Save output to file |

### Output Formats
- `-oN` — Normal text
- `-oX` — XML
- `-oG` — Grepable
- `-oA` — All three at once

---

## Sherlock — Username OSINT

**Purpose:** Search for a username across 300+ social media platforms simultaneously

### Usage

```bash
# Basic search
sherlock username

# Search multiple usernames
sherlock user1 user2 user3

# Save results to file
sherlock username --output results.txt

# Timeout per site (default 60s)
sherlock username --timeout 10
```

### What It Returns
- URL of each platform where the username exists
- Response time per platform
- Sites where username was NOT found are filtered out by default

### Use Cases
- OSINT investigations — mapping a target's online presence
- Username correlation across platforms
- Social engineering research

---

## Holehe — Email OSINT

**Purpose:** Check if an email address is registered on 120+ websites without sending emails

### Usage

```bash
# Basic check
holehe target@email.com

# Export results
holehe target@email.com --only-used > results.txt
```

### How It Works
Holehe uses password reset flows — it submits the email to each site's "forgot password"
function and checks whether the site returns a "user found" or "user not found" response.
No emails are sent to the target.

### Output
- ✅ Sites where the email IS registered
- ❌ Sites where it is NOT registered
- ⚠️ Sites that couldn't be checked (rate limited, down, etc.)

### Use Cases
- Email-based OSINT investigations
- Mapping a target's account footprint from a known email
- Threat intelligence gathering

---

## Wireshark — Packet Analyzer

**Purpose:** Capture and analyze network traffic in real time

### Key Filters

| Filter | What It Shows |
|--------|--------------|
| `ip.addr == 192.168.1.1` | All traffic to/from IP |
| `tcp.port == 80` | HTTP traffic |
| `tcp.port == 443` | HTTPS traffic |
| `dns` | All DNS queries |
| `http` | HTTP requests and responses |
| `tcp.flags.syn == 1` | SYN packets (connection attempts) |

### Common Use Cases
- Detecting unencrypted credentials on the wire
- Identifying suspicious outbound connections
- Analyzing malware network behavior in a sandbox

---

*Part of the [stephen-sec](https://github.com/stephen-sec) cybersecurity portfolio.*
