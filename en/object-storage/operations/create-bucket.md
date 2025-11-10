# Create Bucket

## Create a bucket via Console
1. Console → Object Storage → **Create bucket**
2. Enter name → select region and class
3. Optional:
   - Versioning
   - Lifecycle rules
   - Access policy

## CLI
```bash
fc storage bucket create \
  --name my-bucket \
  --region fc-central1 \
  --storage-class STANDARD
```            
