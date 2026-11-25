# Lab 4 (Week 5): Active Footprinting & Reconnaissance Report

* **Student Name:** Nurul Suhaila Binti Anissufian
* **Student ID:** 52215125568
* **Class / Section:** L01-B01
* **Course:** Computer System Security
* **Assessment Date & Time:** 24 November 2026, ~23:11 – 23:15 +08

---

## Executive Overview & Scope Boundary

This report documents an authorized active footprinting and service enumeration exercise conducted against a single local training web target, **OWASP Juice Shop** (`http://localhost:3000`). The assessment focused strictly on safe, non-destructive reconnaissance of the web service layer, including HTTP response header inspection and service version probing. No exploitation, brute-force attacks, persistence mechanisms, or destructive actions were performed.

| Assessment Parameter | Recorded Details |
| :--- | :--- |
| **Lab Topic** | Lab 4 (Week 5): Active Footprinting & Reconnaissance |
| **Target Application** | OWASP Juice Shop (`http://localhost:3000`) |
| **Attacker Host** | Kali Linux Virtual Machine (`10.0.2.15/24` on `eth0`, loopback `127.0.0.1`) |
| **Assessment Window** | 24 November 2026, ~23:11 – 23:15 +08 |
| **Testing Scope** | Authorized web service reconnaissance only; zero exploitation or disruption |

---

## 1. Own Host Setup (Attacker) 
The reconnaissance commands were executed from a Kali Linux virtual machine. Before probing the target, network interface addresses and routing entries were checked to confirm active interfaces and 
network context. 

![Check Network Interface and Routing Table](Screenshot%202026-11-24%20233136.png)

## 2. Target Setup (Victim) 
The target environment is an intentionally vulnerable web application running locally inside a Docker container on the Kali Linux virtual machine. Hosting the instance locally provides a controlled, predictable training target without relying on external public demo servers 

![OWASP Juice Shop Web Application in Browser](Screenshot%202026-11-24%20231343.png)
• Selected Target: OWASP Juice Shop (Local Docker Instance) 
• Target URL: http://localhost:3000 
• Container Image: bkimminich/juice-shop (published to host port 3000 via -p 3000:3000) 
• Target Address & Port: 127.0.0.1 (localhost), TCP Port 3000 
• Target Type: Intentionally vulnerable web application for authorized security training

## 3. Finding 1: HTTP Response Header Enumeration (curl -I) 
An HTTP HEAD request was sent to http://localhost:3000 to inspect the server status code and response headers without downloading the full response body. 

![Check HTTP Response Headers with curl](Screenshot%202026-11-24%20234101.png)
• Command Executed: curl -I http://localhost:3000 
• Timestamp: Tue, 24 Nov 2026 15:11:51 GMT (23:11:51 +08) 
• What It Proves: At 15:11:51 GMT on 24 November 2026, http://localhost:3000 responded to a HEAD 
request with HTTP/1.1 200 OK, Content-Type: text/html; charset=UTF-8, Content-Length: 9831, and the 
listed response headers. 
• What It Suggests: A web service is actively serving HTML content on port 3000. The custom X-Recruiting: 
/#/jobs header is characteristic of OWASP Juice Shop, while Access-Control-Allow-Origin: * suggests a 
permissive cross-origin policy. 
• What It Cannot Establish: A 200 OK response and HTTP headers do not prove that specific vulnerabilities 
are exploitable, nor do they reveal internal application logic, secrets, or backend configuration.

## 4. Finding 2: Port State & Service Version Enumeration (nmap -sV) 
A targeted Nmap version scan was executed against localhost on TCP port 3000 to check port state and service fingerprint responses. 
![Nmap Service Scan on Port 3000](Screenshot%202026-11-24%20234433.png)

![Nmap Service Fingerprint Output for OWASP Juice Shop](Screenshot%202026-11-24%20234448.png)
• Command Executed: nmap -sV -p 3000 localhost 
• Timestamp: 2026-11-24 23:14 +08 (Tue, 24 Nov 2026 15:14:54 GMT) 
• What It Proves: At 23:14 +08 on 24 November 2026, 127.0.0.1 (localhost) responded with 0.000082s latency, TCP port 3000 was open, and the HTTP probe payload returned HTML containing <title>OWASP Juice Shop</title>. 
• What It Suggests: Despite Nmap's ppp? service label, the returned HTTP response confirms that port 3000 
serves the OWASP Juice Shop web application rather than a PPP service. 
• What It Cannot Establish: Automated service fingerprinting did not cleanly identify the service (1 service unrecognized despite returning data), showing that summary service labels alone cannot be treated as conclusive proof of service type or security vulnerabilities.

