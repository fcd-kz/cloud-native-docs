# Quickstart

## Create a CDN Distribution

1. Go to **Freedom Cloud Console**
2. Choose **CDN**
3. Click **Create distribution**
4. Set:
   - Origin type (Object Storage / Custom HTTP origin)
   - Origin domain or bucket
   - Protocol: HTTP / HTTPS
   - Caching mode: auto / manual
5. Click **Create**

## Test Content Delivery
```
https://<cdn-id>.edge.freedomcloud.net/file.jpg
```

## Purge Cache
```bash
fc cdn purge --distribution-id <ID>
```
