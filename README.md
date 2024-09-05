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
















