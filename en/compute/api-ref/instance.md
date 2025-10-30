# API reference — VM Instance

## Create VM  
```bash
POST /compute/v1/instance
```
### Request body  
```json
{
  "folderId": "<FOLDER_ID>",
  "name": "my-vm",
  "zoneId": "ru-central1-a",
  "resources": {
    "cores": 2,
    "memory": "4GiB"
  },
  "bootDisk": {
    "size": "50GiB",
    "typeId": "network-hdd"
  },
  "networkInterface": {
    "subnetId": "<SUBNET_ID>",
    "natIpVersion": "ipv4"
  },
  "platformId": "standard-v1"
}
```
### Response body
```json
{
  "id": "<INSTANCE_ID>",
  "status": "PROVISIONING",
  "name": "my-vm",
  ...
}
```
