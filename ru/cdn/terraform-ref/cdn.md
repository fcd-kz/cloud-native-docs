# Terraform — CDN

```hcl
resource "freedomcloud_cdn_distribution" "example" {
  name       = "cdn-site"
  origin_url = "https://example.com"
}
```
