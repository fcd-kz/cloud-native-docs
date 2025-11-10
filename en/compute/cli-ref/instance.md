# CLI reference — VM Instance

## List instances  
```bash
fc compute instance list --folder-id <FOLDER_ID>
```
## Get instance details
```bash
fc compute instance get --instance-id <INSTANCE_ID> --folder-id <FOLDER_ID>
```
## Create instance (sample)
```bash
fc compute instance create \
  --folder-id <FOLDER_ID> \
  --name my-vm \
  --zone ru-central1-a \
  --platform standard-v1 \
  --memory 4GiB \
  --cores 2 \
  --network-interface subnet-id=<SUBNET_ID>,nat-ip-version=ipv4
  ```
