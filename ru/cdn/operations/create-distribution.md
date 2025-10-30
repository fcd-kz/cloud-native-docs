# Создание CDN-дистрибутива

## В консоли

1. CDN → **Создать дистрибутив**
2. Заполнить параметры:
   - Название
   - Origin URL или бакет
   - Протокол (HTTP/HTTPS)
3. Сохранить

## CLI

```bash
fc cdn create   --name static-site   --origin-url https://static.example.com
```
