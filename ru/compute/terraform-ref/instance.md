# Terraform — Виртуальные машины

```hcl
resource "freedomcloud_compute_instance" "vm" {
  name   = "vm1"
  cores  = 2
  memory = "4GiB"
}
```
