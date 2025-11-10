# Terraform — CDN

```hcl
resource "freedom_cdn" "site" {
  name = "site-cdn"
  origin_url = "https://example.com"
}
```
