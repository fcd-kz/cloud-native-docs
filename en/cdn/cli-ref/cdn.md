# CLI — CDN

### Create distribution
```bash
fc cdn create --name site-cdn --origin-url https://example.com
```

### List distributions
```bash
fc cdn list
```

### Purge cache
```bash
fc cdn purge --distribution-id <ID>
```
