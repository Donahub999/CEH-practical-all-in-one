# CEH-practical-all-in-one
🔥 WIRESHARK FILTERING – EXAM MASTER LIST

⚠️ These are Display Filters (used in the top filter bar of Wireshark)

🔹 BASIC PROTOCOL FILTERS
tcp
udp
icmp
dns
http
https
ftp
smtp
pop
imap
ssh
telnet
arp

🔹 IP ADDRESS FILTERS
Single IP
ip.addr == 192.168.1.10

Source IP
ip.src == 192.168.1.10

Destination IP
ip.dst == 192.168.1.20

Subnet
ip.addr == 192.168.1.0/24

🔹 PORT FILTERS
Specific port
tcp.port == 80

Source port
tcp.srcport == 8888

Destination port
tcp.dstport == 9999

Multiple ports
tcp.port == 80 || tcp.port == 443

🔹 TCP FLAG FILTERS (VERY IMPORTANT)
SYN packets
tcp.flags.syn == 1 && tcp.flags.ack == 0

SYN-ACK
tcp.flags.syn == 1 && tcp.flags.ack == 1

ACK only
tcp.flags.ack == 1 && tcp.flags.syn == 0

FIN packets
tcp.flags.fin == 1

RST packets
tcp.flags.rst == 1

Possible port scan
tcp.flags.syn == 1 && tcp.flags.ack == 0

🔹 ICMP FILTERS
All ICMP
icmp

Ping request
icmp.type == 8

Ping reply
icmp.type == 0

Large ICMP payload (tunneling)
icmp && frame.len > 100

🔹 DNS FILTERS (EXAM FAVORITE)
All DNS
dns

DNS queries only
dns.flags.response == 0

DNS responses only
dns.flags.response == 1

Domain name search
dns.qry.name contains "google"

🔹 HTTP FILTERS (VERY IMPORTANT)
All HTTP
http

GET requests
http.request.method == "GET"

POST requests
http.request.method == "POST"

URLs
http.request.uri

Specific file download
http.request.uri contains ".exe"

🔹 CREDENTIAL HUNTING 🔐 (EXAM GOLD)
Plaintext passwords
http.authorization

FTP login
ftp.request.command == "USER" || ftp.request.command == "PASS"

Telnet data
telnet

🔹 FOLLOW STREAM FILTERS

After Follow TCP Stream, Wireshark auto-applies:

tcp.stream == 3


Manually:

tcp.stream == 0

🔹 FILE / DATA EXTRACTION
Detect file transfer
http.response.code == 200


Then:

File → Export Objects → HTTP

🔹 MALWARE / ATTACK DETECTION
Suspicious DNS tunneling
dns && strlen(dns.qry.name) > 50

Beaconing (regular intervals)
tcp && frame.time_delta < 1

Large packets (data exfiltration)
frame.len > 1000

🔹 Covert / Steganography RELATED (your use-case)
Custom port covert channel
tcp.port == 8888

IP ID analysis (covert_tcp)
ip.id

TCP sequence anomalies
tcp.seq

🔹 COMBINED FILTERS (ADVANCED)
Traffic from IP on port 80
ip.src == 10.0.0.5 && tcp.port == 80

Suspicious SYN scan from one IP
ip.src == 192.168.1.5 && tcp.flags.syn == 1 && tcp.flags.ack == 0

🔹 TIME-BASED FILTERING
Slow attack / beaconing
frame.time_delta > 5

🔹 STATISTICS-BASED (EXAM QUESTIONS)
Statistics → Protocol Hierarchy
Statistics → Endpoints
Statistics → Conversations
Statistics → IO Graphs

🧠 MUST-REMEMBER FOR EXAM
Topic	Priority
TCP flags	⭐⭐⭐⭐⭐
DNS filters	⭐⭐⭐⭐⭐
HTTP GET/POST	⭐⭐⭐⭐
Follow TCP Stream	⭐⭐⭐⭐⭐
File extraction	⭐⭐⭐⭐
ICMP tunneling	⭐⭐⭐
🚀 PRACTICE TASK FOR YOU (DO THIS NOW)

Capture traffic using:

sudo tcpdump -i any -w test.pcap


Open in Wireshark

Apply:

dns
tcp.flags.syn == 1
http.request

