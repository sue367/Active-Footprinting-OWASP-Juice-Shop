# Lab 4 (Week 5): Active Footprinting & Reconnaissance Report

* **Student Name:** Nurul Suhaila Binti Anissufian
* **Student ID:** 52215125568
* **Class / Section:** L01-B01
* **Course:** Computer System Security
* **Assessment Date & Time:** 24 November 2026, ~23:11 – 23:15 +08

---

## 1. Executive Overview & Scope Boundary

This report documents an authorized active footprinting and service enumeration exercise conducted against a single local training web target, **OWASP Juice Shop** (`http://localhost:3000`). The assessment focused strictly on safe, non-destructive reconnaissance of the web service layer, including HTTP response header inspection and service version probing. No exploitation, brute-force attacks, persistence mechanisms, or destructive actions were performed.

| Assessment Parameter | Recorded Details |
| :--- | :--- |
| **Lab Topic** | Lab 4 (Week 5): Active Footprinting & Reconnaissance |
| **Target Application** | OWASP Juice Shop (`http://localhost:3000`) |
| **Attacker Host** | Kali Linux Virtual Machine (`10.0.2.15/24` on `eth0`, loopback `127.0.0.1`) |
| **Assessment Window** | 24 November 2026, ~23:11 – 23:15 +08 |
| **Testing Scope** | Authorized web service reconnaissance only; zero exploitation or disruption |

---

## 2. Target Setup (Victim)

The target environment is an intentionally vulnerable web application running locally inside a Docker container on the Kali Linux virtual machine. Hosting the instance locally provides a controlled, predictable training target without relying on external public demo servers.

* **Selected Target:** OWASP Juice Shop (Local Docker Instance)
* **Target URL:** `http://localhost:3000`
* **Container Image:** `bkimminich/juice-shop` (published to host port `3000` via `-p 3000:3000`)
* **Target Address & Port:** `127.0.0.1` (`localhost`), TCP Port `3000`
* **Target Category:** Intentionally vulnerable web application for authorized security training


---

## 3. Own Host Setup (Attacker)

The reconnaissance commands were executed from a Kali Linux virtual machine. Before probing the target, network interface addresses and routing entries were checked to confirm active interfaces and network context.

* **Operating System:** Kali Linux (VirtualBox Virtual Machine)
* **Network Adapter Configuration:** VirtualBox NAT (`10.0.2.0/24` subnet)
* **Commands Executed:**

```bash
ip -br addr
ip route
