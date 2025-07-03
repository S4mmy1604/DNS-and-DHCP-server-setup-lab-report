# DNS-and-DHCP-server-setup-lab-report
DNS and DHCP Server Setup Lab Report
Objective
Set up a local DNS and DHCP server lab environment using Ubuntu Server and Kali Linux in VirtualBox to learn and practice network services configuration, management, and troubleshooting.

Environment Setup
Host machine: [Your OS]

Virtualization: Oracle VirtualBox

VMs:
Ubuntu Server (DNS & DHCP server)
Kali Linux (Client machine for testing)

Steps Performed
1. Ubuntu Server Preparation
- Installed Ubuntu Server in VirtualBox with network adapter set to Internal Network.
- Configured static IP for Ubuntu Server (e.g., 192.168.56.10).
- Installed and configured BIND9 DNS server.
- Created forward and reverse DNS zone files for domain lab.local.
- Configured BIND9 zone files with appropriate A and PTR records.
- Incremented zone serial numbers after each modification.
- Restarted BIND9 service and validated DNS configuration using named-checkzone.
- Tested DNS resolution from Ubuntu Server itself.

2. DHCP Server Setup on Ubuntu
Installed and configured ISC DHCP Server.

Configured DHCP to serve IP range 192.168.56.20 - 192.168.56.30.

Set DHCP options including routers (gateway) and DNS server address.

Enabled DHCP server on the correct network interface.

Restarted and verified DHCP server status.

3. Kali Linux Client Configuration
Configured Kali network adapter to the same Internal Network as Ubuntu.

Obtained IP address dynamically via DHCP from Ubuntu Server.

Verified IP assignment with ip a.

Tested network connectivity to Ubuntu Server using ping.

Performed DNS lookups against the Ubuntu BIND DNS server.

Confirmed forward and reverse DNS resolution.

Troubleshooting and Fixes
Reset and corrected DNS zone records to match dynamic IP assigned by DHCP.

Incremented DNS zone serial numbers on every zone file change to propagate updates.

Resolved network interface issues by matching VirtualBox network adapter settings on both VMs.

Addressed Kali Linux missing DHCP client tools by leveraging system defaults and rebooting.

Learnings and Notes
DNS and DHCP must be configured carefully with matching IP ranges and hostnames.

BIND9 requires zone files to have properly formatted forward and reverse zones.

DHCP server must be authoritative for the subnet to assign IPs correctly.

Kali Linux uses continuous ping by default; use -c to limit packets.

Restarting networking services and VMs helps apply network configuration changes.

Understanding network interface names and VirtualBox network modes is crucial for inter-VM communication.

Next Steps
Monitor and analyze DNS and DHCP traffic using Wireshark.

Configure logging for DNS and DHCP servers.

Explore DNS security features such as DNSSEC.

Simulate network attacks and defenses in the lab.

Expand lab with more VMs and services.

Commands Reference
BIND9 commands
bash
Copy
Edit
sudo systemctl restart bind9
sudo named-checkzone lab.local /etc/bind/zones/db.lab.local
sudo named-checkzone 56.168.192.in-addr.arpa /etc/bind/zones/db.192.168.56
DHCP commands
bash
Copy
Edit
sudo systemctl restart isc-dhcp-server
sudo systemctl status isc-dhcp-server
Kali commands
bash
Copy
Edit
ip a
ping 192.168.56.10
nslookup kali.lab.local 192.168.56.10
ping -c 4 kali.lab.local
