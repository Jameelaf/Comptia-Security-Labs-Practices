Using Traceroute in Linux

Lab Objective:
Learn how to use Traceroute in Linux to trace the route to a host.

Lab Purpose:
Traceroute is used to trace the route to a host. This is useful for finding out if the host is up, where the host is located, and how many hops the server is away from you.

Lab Tool:
Kali Linux

Lab Topology:
We will use Kali Linux for this lab.

Lab Walkthrough:

Task 1:
To install traceroute on Kali Linux, simply open a terminal and type the following:
sudo apt-get install traceroute

In this lab, we will demonstrate how this tool works by using Kali Linux. Begin by opening a terminal window. It is important to note that we can use “traceroute” for any host as it is considered public knowledge. Therefore, we can use any site as our target site for this lab without being “root” user.
We will begin by targeting a big site such as “facebook.com”. Type the following:
traceroute facebook.com

<img width="965" alt="Screenshot 2024-09-05 at 5 28 22 PM" src="https://github.com/user-attachments/assets/421fb502-7f73-449b-bbe0-384a7c71542a">

#1 Hostname and IP address which is obtained by reverse DNS Lookup.
#2 30 hops meam traceroute will only route the first 30 hops between your system and victim's system.
#3 This is our first router;possibly modem, router.
#4 Those thre columns display the round trip times (to reach to that point and return to our computer).
#5 Obviously the first column and simply the number of hops .
#6 Our destination, wehre it has the same IP address as the first line.


<img width="965" alt="Screenshot 2024-09-05 at 5 28 00 PM" src="https://github.com/user-attachments/assets/73d75f0f-ee00-4d55-b403-e8ee295dd302">

<img width="965" alt="Screenshot 2024-09-05 at 5 28 07 PM" src="https://github.com/user-attachments/assets/c1b9889f-e1c5-4b83-9da0-972caf2d2b88">

Sometimes we tend to get missing responce like these stars. Why??

Reasons for Missing Responses

ICMP or UDP Blocking:
Many routers on the internet are configured to block ICMP "Time Exceeded" messages or simply drop ICMP or UDP packets sent by traceroute. As a result, these hops appear as * * * in the output.

Firewall Restrictions:
Firewalls on the routers or network devices may block traceroute packets, especially on the networks of major service providers like Facebook. This is often done for security and to prevent network reconnaissance.

Asymmetric Routing:
Some networks use asymmetric routing, meaning that the path from the source to the destination is different from the path from the destination back to the source. This can cause some hops to appear unreachable.


What can we do? Use alternative methods....

Use different protocol: Try using traceroute with ICMP (like Windows' tracert) instead of the default UDP on Linux. This can be done using the -I option: traceroute -I facebook.com 

Check with Different Destinations: Run traceroute to a different domain or IP to see if you get a different output. This can help determine if the issue is specific to Facebook's network.

Key Concepts:

Private IP Addresses:
These are IP addresses used within private networks (such as home networks, corporate LANs, etc.) and are not routable on the public internet

Common Private IP Ranges:
10.0.0.0 to 10.255.255.255
172.16.0.0 to 172.31.255.255
192.168.0.0 to 192.168.255.255

Public IP Addresses:
These are routable IP addresses that are assigned to devices that can be accessed over the internet. They are globally unique and managed by the Internet Assigned Numbers Authority (IANA).

Boundary Between Private and Public Networks:
The boundary is the point where traffic leaves your local network and enters the public internet. It usually occurs at the router or gateway that connects your home or private network to your Internet Service Provider (ISP).

Lets analyze a traceroute Output:

traceroute to google.com (64.233.170.101), 30 hops max, 60 byte packets
 1  10.0.2.1 (10.0.2.1)  0.628 ms  0.669 ms *
 2  192.168.10.1 (192.168.10.1)  3.613 ms  3.499 ms *
 3  1.128.212.218.starhub.net.sg (218.212.128.1)  7.575 ms  9.184 ms *
 4  183.90.44.193 (183.90.44.193)  10.084 ms  9.757 ms *
 5  203.118.7.77 (203.118.7.77)  10.740 ms * *
 6  203.118.60.29 (203.118.60.29)  9.938 ms * *
 7  203.118.6.149 (203.118.6.149)  6.480 ms * *
 8  203.116.3-102.unknown.starhub.net.sg (203.116.3.102)  7.712 ms * *
 9  142.250.166.50 (142.250.166.50)  9.045 ms * *
10  142.250.238.115 (142.250.238.115)  7.779 ms * *
11  192.178.109.86 (192.178.109.86)  7.403 ms * *
12  * * *
13  142.251.231.253 (142.251.231.253)  42.438 ms  31.949 ms  31.529 ms
14  142.251.247.203 (142.251.247.203)  7.791 ms  9.000 ms  8.348 ms
15  * * *
...................

Explanation of the Output
Hop 1 (10.0.2.1):
Private IP (10.0.2.1): This is the first router or gateway on your local network. The packet is still within your private network.

Hop 2 (192.168.10.1):
Private IP (192.168.10.1): This is another device or gateway on your local network or ISP's local network. The packet is still within a private IP range.

Hop 3 (218.212.128.1):
Public IP (218.212.128.1): The packet has left the private network and has entered the ISP's public network. This marks the boundary between your home network and the ISP/public network.

Hops 4 to 14:
Public IPs: These are routers on the public internet, belonging to various ISPs and network providers that route the packet toward Google's network.

Hop 15 and Beyond:
The * * * indicates that the request timed out or that these devices are configured not to respond to ICMP echo requests/maybe blocked by a firewall.

Summary
Boundary Crossing: The boundary from your home network to the public network happens at Hop 3 (218.212.128.1). This is where the packet leaves the private network (with private IP addresses like 10.0.2.1 and 192.168.10.1) and enters the ISP's public network.
Private IPs are seen in the first two hops, indicating the packet is still within a private network.
Public IPs appear from Hop 3 onward, indicating the packet is now traversing through public networks across different ISPs until it reaches its destination (google.com).

<img width="913" alt="Screenshot 2024-09-05 at 5 36 44 PM" src="https://github.com/user-attachments/assets/8b139a9e-a6ff-4957-89be-2b534b1add88">






