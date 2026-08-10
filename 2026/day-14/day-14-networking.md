# Day 14 – Networking Fundamentals & Hands-on Checks

## Task
Get comfortable with core networking concepts and the commands you'll actually run during troubleshooting.

**Covers:**
- Mapping OSI vs TCP/IP models in your own words
- Running essential connectivity commands
- Capturing a mini network check for a target host/service

---

## OSI vs TCP/IP

**OSI Model → 7 layers** (Physical → Application)

| Layer | Name |
|---|---|
| A | Application |
| P | Presentation |
| S | Session |
| T | Transport |
| N | Network |
| D | Data Link |
| P | Physical |

**Mnemonic:** *"Aree Pagali Saath Toh Nibha Deti Pyaari"* (A-P-S-T-N-D-P) 😄

**TCP/IP Model → 4 layers** (Link, Internet, Transport, Application)

| Layer | Name |
|---|---|
| A | Application |
| T | Transport |
| I | Internet |
| N | Network Access |

**Mnemonic:** just remember **"NITA Ambani"** (N-I-T-A)

**Where common protocols sit:**
- IP → Internet layer
- TCP/UDP → Transport layer
- HTTP/HTTPS → Application layer
- DNS → Application layer

**Example:** `curl https://google.com` → HTTP over TCP over IP

<img width="1849" height="352" alt="image" src="https://github.com/user-attachments/assets/a59099ff-bc87-441f-91f2-b18cf6a9e83b" />



---

## Hands-on Checklist

Run each, with a short observation:

| Check | Command | What to note |
|---|---|---|
| Identity | `hostname -I` (or `ip addr show`) | Your IP |
| Reachability | `ping <target>` | Latency and packet loss |
| Path | `traceroute <target>` (or `tracepath`) | Long hops/timeouts |
| Ports | `ss -tulpn` (or `netstat -tulpn`) | One listening service and its port |
| Name resolution | `dig <domain>` or `nslookup <domain>` | Resolved IP |
| HTTP check | `curl -I <http/https-url>` | HTTP status code |
| Connections snapshot | `netstat -an \| head` | Rough count of ESTABLISHED vs LISTEN |

Pick one target service/host (e.g. `google.com`, a lab server, or a local service) and stick with it for ping/traceroute/curl where possible.

<img width="808" height="327" alt="image" src="https://github.com/user-attachments/assets/58374545-bd3d-42cc-8dcc-c48cf41ddbda" />

<img width="1263" height="337" alt="image" src="https://github.com/user-attachments/assets/64455ab2-a155-4ebd-a0b3-0cb6261760f8" />

<img width="710" height="242" alt="image" src="https://github.com/user-attachments/assets/62d2bbbc-3d81-4649-a91e-c4373b4921d4" />

<img width="664" height="830" alt="image" src="https://github.com/user-attachments/assets/f18795b6-cd05-419c-995e-aa864ff2681b" />

<img width="1849" height="352" alt="image" src="https://github.com/user-attachments/assets/960344a4-7b6d-402f-938e-32ecd1f2fa14" />

<img width="742" height="247" alt="image" src="https://github.com/user-attachments/assets/10f62fcb-1ea3-4ec5-b73b-05552f7a1b72" />

---

## Mini Task: Port Probe & Interpret

1. Identify one listening port from `ss -tulpn` (e.g. SSH on 22, or a local web app)
2. Test it from the same machine: `nc -zv localhost <port>` (or `curl -I http://localhost:<port>`)
3. Note: is it reachable? If not, what's the next check (service status, firewall, etc.)?
<img width="750" height="433" alt="image" src="https://github.com/user-attachments/assets/29d88491-e280-4905-8ec9-daddcebdd200" />


---

## Reflection

**Fastest command:** `ping` — quickest way to confirm the system is reachable

**If DNS fails:** check the DNS layer with `dig`

**If HTTP 500:** check application logs (application layer issue)

**Next checks:**
1. `systemctl status <service>`
2. `journalctl` logs
