# Networking

VM instances connect to a Virtual Private Cloud (VPC) network. You assign:

- Subnet (private IP range)  
- Optional public IP address  
- Route tables, NAT gateway, firewall/security groups

### Public & Private IPs  
- Private IP: free, internal communication  
- Public IP: optional, billed hourly when allocated

### Security groups & firewall rules  
Set inbound/outbound rules to control traffic.  
Example: allow SSH (TCP 22) from trusted IPs, disable all other inbound by default.
