# Configure Cache Rules

| Rule | Behavior |
|---|---|
Cache static files | `.css, .js, .png, .jpg, .svg` |
Disable cache for APIs | `/api/*` |
Custom TTL | override default cache time |

### Purge Cache
```bash
fc cdn purge --distribution-id <ID>
```
