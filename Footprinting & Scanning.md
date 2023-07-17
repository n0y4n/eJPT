# Footprinting & Scanning
#### For this, You need to MAP the network by using the following tools:
1. Arp-scan
      - https://www.kali.org/tools/arp-scan/
2. Ping
3. Fping
      - https://fping.org/
4. Nmap
      - https://www.kali.org/tools/nmap/
5. zenmap
      - https://nmap.org/zenmap/

#### You should also perform a port scan in order to identify the OS and services using Nmap or the following tools:
-   **Nmap:**
    -   To scan all ports:  `nmap -p- 192.168.0.1`
    -   To scan a single port:  `nmap -p 22 192.168.1.1`
    -   To scan a range of ports:  `nmap -p 1-100 192.168.1.1`
-   **Zenmap:**
    -   To scan all ports:  `zenmap -p- 192.168.0.1`
    -   To scan a single port:  `zenmap -p 22 192.168.1.1`
    -   To scan a range of ports:  `zenmap -p 1-100 192.168.1.1`
-   **Automator:**
    -   To scan all ports:  `automator -p- 192.168.0.1`
    -   To scan a single port:  `automator -p 22 192.168.1.1`
    -   To scan a range of ports:  `automator -p 1-100 192.168.1.1`
-   **Masscan:**
    -   To scan all ports:  `masscan -p- -iL hosts.txt`
    -   To scan a single port:  `masscan -p 22 -iL hosts.txt`
    -   To scan a range of ports:  `masscan -p 1-100 -iL hosts.txt`
-   **Rustscan:**
    -   To scan all ports:  `rustscan -p- 192.168.0.1`
    -   To scan a single port:  `rustscan -p 22 192.168.1.1`
    -   To scan a range of ports:  `rustscan -p 1-100 192.168.1.1`
-   **Autorecon:**
    -   To scan all ports:  `autorecon -p- 192.168.0.1`
    -   To scan a single port:  `autorecon -p 22 192.168.1.1`
    -   To scan a range of ports:  `autorecon -p 1-100 192.168.1.1`
