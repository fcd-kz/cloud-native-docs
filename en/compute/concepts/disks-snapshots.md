# Disks & Snapshots

## Disks  
Every VM must have a boot disk. You can also attach additional data disks for storage or application data. Disks come in types: SSD and HDD.  
Disks are automatically replicated within the availability zone for durability.

## Snapshots & Images  
- **Snapshot** — point-in-time copy of a disk.  
- **Image** — reusable bootable template created from a disk or snapshot.

You can create an image from a snapshot and deploy new VM instances from that image — standardising configurations across your fleet.
