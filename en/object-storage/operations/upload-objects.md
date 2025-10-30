# Upload & Manage Objects

## Upload
```bash
fc storage object upload \
  --bucket my-bucket \
  --file backup.tar.gz \
  --key backups/backup.tar.gz
```
## List objects
```bash
fc storage object list --bucket my-bucket
```

## Download
```bash
fc storage object download \
  --bucket my-bucket \
  --key backups/backup.tar.gz \
  --file ./backup.tar.gz
```

## Delete
```bash
fc storage object delete \
  --bucket my-bucket \
  --key old/photo.png
```
