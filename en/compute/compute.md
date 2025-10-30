# Virtual Machines (Compute)

## Overview  
The Virtual Machines service provides scalable and flexible compute instances for running applications, services, and workloads. You can choose from predefined machine types, create custom configurations, use Linux or Windows images, and integrate with network, storage, and security services.

## Key Capabilities  
- Wide range of machine types (vCPU + RAM)  
- Flexible boot and data disks (SSD / HDD)  
- Private and public network interfaces  
- SSH (Linux) / RDP (Windows) access  
- Security groups and firewall configuration  
- Snapshots, custom images, auto-scaling support  
- Integration with Virtual Private Cloud (VPC) and object storage  

## Pricing  
Billing is based on usage. The following table gives example pricing components:

| Resource         | Pricing model            |
|------------------|--------------------------|
| vCPU             | ≈ US$ 0.012 per vCPU-hour |
| RAM              | ≈ US$ 0.004 per GB-hour   |
| Storage (SSD)    | ≈ US$ 0.09 per GB-month   |
| Public IP address| ≈ US$ 0.003 per hour      |
| Egress traffic   | ≈ US$ 0.02 per GB         |

**Example:** A 2-vCPU, 4 GB RAM VM running continuously (~730 h/month) would cost ≈ US$ 0.032/hour (~US$ 23/month).

## Quotas & Limits  
| Resource          | Default limit           |
|-------------------|-------------------------|
| Maximum VMs       | 20 per project          |
| Maximum vCPU      | 80 per project          |
| Maximum RAM       | 300 GB per project      |
| Public IP addresses| 10 per project         |

> *Note:* To increase quotas, submit a support request.  

## Getting Started  
1. Open the Cloud Portal and navigate to **Compute → Virtual Machines**.  
2. Click **Create VM**.  
3. Configure the following:  
   - Select image (Linux/Windows)  
   - Choose machine type (vCPU + RAM)  
   - Specify boot disk size & type  
   - Connect network: VPC, subnet, optional public IP  
   - Set SSH key (Linux) or RDP user/password (Windows)  
   - (Optional) Configure tags, metadata, auto scaling  
4. Deploy the VM. After status changes to **RUNNING**, connect via SSH/RDP.  
5. Monitor resource usage, apply security groups, take snapshots as needed.

---

## Additional Topics  
### Custom images & snapshots  
You can create snapshots of disks and use them to create custom images, enabling you to standardise deployments and apply your organisation’s configuration.  
### Networking & security  
Assign your VM to a VPC, configure private IPs, NAT-gateway, firewall rules and security groups for inbound/outbound traffic control.  
### Autoscaling & instance groups  
Define instance groups and autoscaling policies to automatically add or remove VM instances based on load metrics (CPU, memory, network) or schedule.  
### Billing optimisation tips  
- Use preemptible instances (if available) for cost-sensitive workloads  
- Choose correct machine size: avoid over-provisioning  
- Turn off unused instances to avoid idle cost  
- Monitor egress traffic and choose proper region to reduce cost  

---

*Last updated: 2025-10-30*
