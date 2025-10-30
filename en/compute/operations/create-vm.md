# Create a VM

This guide shows how to create a virtual machine in Freedom Cloud.

## Steps  
1. Navigate to Portal → **Compute → Virtual Machines**.  
2. Click **Create VM**.  
3. On the “Configuration” tab:  
   - Select OS image (Linux/Windows)  
   - Choose machine type (e.g., 2 vCPU + 4 GB RAM)  
   - Set boot disk size/type (SSD/HDD)  
   - (Optional) Add data disks  
4. On the “Network” tab:  
   - Select VPC and subnet  
   - Enable public IP if needed  
   - Configure firewall/security group  
5. On the “Access” tab:  
   - Provide SSH key (for Linux) or RDP credentials (for Windows)  
6. Click **Deploy**.  
7. Wait until the status shows **RUNNING**.  
8. Connect and verify the VM is operational.

## Next steps  
- Take a snapshot of the boot disk  
- Add to instance group or enable auto-scaling  
- Monitor resource usage via Portal
