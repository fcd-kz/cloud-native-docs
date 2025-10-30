# FAQ

**Q: What happens if I stop a VM?**  
**A:** When a VM is stopped, you are not billed for vCPU or RAM; you only pay for attached disks and any allocated public IPs.

**Q: Can I migrate a VM between zones?**  
**A:** Yes — you can create a snapshot of the VM or disk and then deploy a new VM in the target zone. Direct live migration between zones is not supported.

**Q: Are public IP addresses billed when VM is stopped?**  
**A:** Yes — if the public IP remains allocated, hourly charges for that IP still apply, even if the VM is stopped.
