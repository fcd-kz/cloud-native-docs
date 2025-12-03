# Quickstart

## Create a Bucket
1. Open **Freedom Cloud Console**
2. Go to **Object Storage → Buckets**
3. Click **Create bucket**
4. Choose:
   - Bucket name (globally unique)
   - Region
   - Storage class (Standard / Cold / Archive)
5. Click **Create**

## Upload an Object
### Console
Go to your bucket → **Upload object** → select file.

### CLI
```bash
fc storage object upload --bucket my-bucket --file ./photo.jpg --key photo.jpg
```
### Access the File

For private objects — generate a signed URL

For public assets — enable public read ACL or CDN
```bash
fc storage object url --bucket my-bucket --key photo.jpg --public
```
