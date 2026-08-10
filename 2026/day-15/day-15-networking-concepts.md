# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Task
Build on Day 14 by understanding the building blocks of networking every DevOps engineer must know: DNS resolution, IP addressing, CIDR/subnetting, and common ports. Concept-focused — researched and documented in my own words.

---

## Task 1: DNS – How Names Become IPs

**What happens when you type `google.com` in a browser?**
The browser sends a request → DNS resolves the domain (`google.com`) to an IP → a connection is made to that server → the server returns the response. The resolved IP belongs to the machine hosting the Google website.

**Record types:**

| Record | What it does |
|---|---|
| **A** | Connects a domain to an IPv4 address (e.g. `google.com → 142.250.x.x`) |
| **AAAA** | Connects a domain to an IPv6 address (newer, longer format) |
| **CNAME** | Points one domain to another — acts like an alias/shortcut |
| **MX** | Specifies where emails should be routed for that domain |
| **NS** | Specifies which DNS servers manage the domain |

**`dig google.com`** — identifies the A record and TTL from the output.

---

## Task 2: IP Addressing

**What is IPv4?**
A protocol used to identify devices on a network and route internet traffic. Structured as four 8-bit octets, each ranging 0–255 (e.g. `192.168.1.1`) — 4 × 8 = 32 bits total.

**Public vs Private IPs:**

| | Public (e.g. `8.8.8.8`) | Private (e.g. `192.168.2.3`) |
|---|---|---|
| Accessibility | Accessible from anywhere on the internet | Not accessible from the internet |
| Uniqueness | Must be globally unique | Can be reused across many networks |
| Assigned by | ISP / cloud provider (AWS, etc.) | Used internally — home, office, VPC |

**Private IP ranges:**
- `10.x.x.x`
- `172.16.x.x` – `172.31.x.x`
- `192.168.x.x`

**`ip addr show`** — confirms local IP is private.

**Why private IPs exist:**
IPv4 has roughly 4.3 billion total addresses, but the number of devices needing addresses is far larger. Solution: use private IPs inside networks, and represent many devices behind a single public IP.

---

## Task 3: CIDR & Subnetting

1. **`/24` in `192.168.1.0/24`** — denotes the subnet size / number of available addresses.
2. **Usable hosts:**
   - `/24` → 2⁸ = 256 total, 254 usable (first and last reserved)
   - `/16` → 65,536 total, 65,534 usable
   - `/28` → 2⁴ = 16 total, 14 usable
3. **Why subnet?** To divide a network into smaller networks for efficient IP usage and traffic management. Analogy: one house with no rooms vs. dividing it into rooms, each assigned to a person (device).
4. **Reference table:**

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
|------|-------------|-----------|--------------|
| /24  | 255.255.255.0   | 256   | 254   |
| /16  | 255.255.0.0     | 65536 | 65534 |
| /28  | 255.255.255.240 | 16    | 14    |

---

## Task 4: Ports – The Doors to Services

**What is a port?**
An entry point for a service. Analogy: IP is the building, port is the room number.

**Common ports:**

| Port | Service |
|------|---------|
| 22   | SSH     |
| 80   | HTTP    |
| 443  | HTTPS   |
| 53   | DNS     |
| 3306 | MySQL   |
| 6379 | Redis   |
| 27017| MongoDB |

**`ss -tulpn`** — observed SSH running on port 22 and DNS running on port 53.

---

## Task 5: Putting It Together

**`curl http://myapp.com:8080` — which concepts are involved?**
DNS resolution → IP lookup → TCP connection → HTTP request.

**App can't reach a database at `10.0.1.50:3306` — first checks:**
- Check which port is listening: `ss -tulpn`
- Test reachability: `ping 10.0.1.50`
- Check the service status: `systemctl status <service_name>`

---

## What I Learned
- What IP, subnet, and subnet mask mean
- Which services run on which ports
- The difference between public and private IPs
