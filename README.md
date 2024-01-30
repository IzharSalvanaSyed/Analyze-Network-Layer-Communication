# Analyze-Network-Layer-Communication
Analyze DNS and ICMP (Internet Control Message Protocol) traffic in transit using data from a network protocol analyzer tool. You will identify which network protocol was utilized in assessment of the cybersecurity incident.

### Scenario:
You are a cybersecurity analyst working at a company that specializes in providing IT services for clients. Several customers of clients reported that they were not able to access the client company website, www.yummyrecipesforme.com, and saw the error “destination port unreachable” after waiting for the page to load. 

You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you visit the website and you also receive the error “destination port unreachable.” Next, you load your network analyzer tool, tcpdump, and load the webpage again. This time, you receive a lot of packets in your network analyzer. The analyzer shows that when you send UDP packets and receive an ICMP response returned to your host, the results contain an error message: “UDP port 53 unreachable.” 


### Tcpdump results:
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A?  
yummyrecipesforme.com (24)  
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2  
udp port 53 unreachable length 254  

13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A?  
yummyrecipesforme.com (24)  
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2  
udp port 53 unreachable length 320  

13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A?  
yummyrecipesforme.com (24)  
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2  
udp port 53 unreachable length 150  

### Understanding Tcpdump results
In the first line of the log file, you can see the outgoing request from your computer to the DNS server to request the IP address of yummyrecipesforme.com, which is sent in a UDP packet. The First sequence of numbers, 13:24:32.192571, represents the timestamp of the request in 24-hour time. 13:24:32.192571 equates to 1:24 pm and 32 seconds in a 12-hour timeframe. Your computer's IP address is seen after IP 192.51.100.15.52444. To the right of the great sign symbol (>) is the destination IP address, 203.0.113.2.domain, in this case, the IP address of the DNS server. The second and third lines of the log show the initial ICMP request packet. Since the request, the ICMP packet is returning the IP of the DNS server; this means that the ICMP packet was not delivered to the port of the DNS server. The next line after that shows which protocol and port was used. This is seen in "udp port 53 unreachable." The UDP protocol was used to request a DNS using the address of the DNS server, 203.0.113.2.domain, through port 53. The words "unreachable" indicated that the message did not go through to the DNS server. Your browser was not able to obtain the IP address of yummyrecipesforme.com.

### Report
Summary of the problem found in the DNS and ICMP traffic Log:  
The findings indicate that the DNS server is inaccessible or not functioning due to the error message "udp port 53 unreachable." Port 53 is associated with DNS protocol communication.

### Analysis of the data and causes of the incident
A "destination port unreachable" message was recieved while attempting to access the website. Using TCPdump, it revealed that the DNS port 53 was not accessible. This can be due to a firewall blockage of traffic to port 53 or the DNS server experiencing issues. Potential causes for the DNS server's unavailability can be from a successful Denial of Service Attack or the firewall, server was not configured correctly. 
