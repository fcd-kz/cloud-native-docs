# Create CDN Distribution

## Console
1. **CDN → Create distribution**
2. Enter name
3. Select origin type (Object Storage / HTTP server)
4. Configure HTTPS & cache rules
5. Click **Create**

## CLI
```bash
fc cdn create   --name my-site-cdn   --origin-url https://storage.freedomcloud.net/mybucket
```
