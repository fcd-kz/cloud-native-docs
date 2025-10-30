# VM instance

A **VM instance** is a compute resource allocated for your workload in Freedom Cloud. It consists of:

- Processor resources (vCPU)  
- Memory (RAM)  
- Boot disk and optional data disks  
- Network interface(s)  
- Operating system (Linux/Windows)  
- Region & availability zone placement

Instances reside in a **project**, belong to a **folder** and are subject to quotas. Each VM has a unique ID and name (2-63 characters, lowercase letters, numbers, hyphens; must start with a letter, cannot end with hyphen).

### States  
- **PROVISIONING** — being created  
- **RUNNING** — active and accessible  
- **STOPPED** — powered off, storage still billed  
- **TERMINATED** — deleted

### Machine types  
You can choose from predefined machine types (e.g., 1 vCPU + 2 GB RAM, 2 vCPU + 4 GB RAM) or custom configuration (specify vCPU + RAM directly) depending on region availability.
