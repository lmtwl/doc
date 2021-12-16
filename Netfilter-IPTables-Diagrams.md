# Linux NetFilter, IP Tables and Conntrack Diagrams

## IPTABLES TABLES and CHAINS

### IPTables has the following 4 built-in tables.

**1) Filter Table**

Filter is default table for iptables. So, if you don’t define you own table, you’ll be using filter table. Iptables’s filter table has the following built-in chains.

* INPUT chain – Incoming to firewall. For packets coming to the local server.
* OUTPUT chain – Outgoing from firewall. For packets generated locally and going out of the local server.
* FORWARD chain – Packet for another NIC on the local server. For packets routed through the local server.

**2) NAT table**

Iptable’s NAT table has the following built-in chains.

* PREROUTING chain – Alters packets before routing. i.e Packet translation happens immediately after the packet comes to the system (and before routing). This helps to translate the destination ip address of the packets to something that matches the routing on the local server. This is used for DNAT (destination NAT).
* POSTROUTING chain – Alters packets after routing. i.e Packet translation happens when the packets are leaving the system. This helps to translate the source ip address of the packets to something that might match the routing on the desintation server. This is used for SNAT (source NAT).
* OUTPUT chain – NAT for locally generated packets on the firewall.

**3) Mangle table**

Iptables’s Mangle table is for specialized packet alteration. This alters QOS bits in the TCP header. Mangle table has the following built-in chains.

* PREROUTING chain
* OUTPUT chain
* FORWARD chain
* INPUT chain
* POSTROUTING chain

**4) Raw table**

Iptable’s Raw table is for configuration excemptions. Raw table has the following built-in chains.


![](https://cloud.githubusercontent.com/assets/1711674/8742360/87f429c4-2c32-11e5-8535-5a99d5149ff3.gif)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742361/87f7efa0-2c32-11e5-9ece-fbd39411371c.gif)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742362/87fa6654-2c32-11e5-84d6-3ca58dda0a8d.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742353/87ddb284-2c32-11e5-9c9b-bca491c8d0e3.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742356/87e025d2-2c32-11e5-8d62-50f9baf4bc81.gif)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742352/87da5f4e-2c32-11e5-8a90-25fc6158e2a3.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742354/87ddfe2e-2c32-11e5-9146-4d10906b745f.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742351/87d3d85e-2c32-11e5-9f6e-7bcf4728d0fd.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742355/87df7934-2c32-11e5-9bc4-e1cc04da5427.gif)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742357/87e8b72e-2c32-11e5-997a-c6d081186da5.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742358/87ee94aa-2c32-11e5-84b7-4819a676129a.gif)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742359/87f1e966-2c32-11e5-9f65-90ae592bf8c0.png)
---
![](https://cloud.githubusercontent.com/assets/1711674/8742363/87fad710-2c32-11e5-8896-7adf1a4cf164.png)
