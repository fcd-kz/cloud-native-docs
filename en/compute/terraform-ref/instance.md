# Terraform reference — VM Instance

```hcl
resource "freedomcloud_compute_instance" "vm1" {
  folder_id    = var.folder_id
  name         = "my-vm"
  zone         = "zone-1a"
  cores        = 2
  memory       = "4GiB"
  boot_disk {
    size = "50GiB"
    type = "ssd"
  }
  network_interface {
    subnet_id       = var.subnet_id
    nat_ip_version  = "ipv4"
  }
  platform = "standard-v1"
}
```
