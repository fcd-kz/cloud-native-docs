# Terraform Example — Object

```hcl
resource "freedom_object" "file" {
  bucket = freedom_bucket.example.name
  key    = "app.zip"
  source = "./app.zip"
}
```
