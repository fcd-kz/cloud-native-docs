# Создать виртуальную машину

## Через портал

1. Compute → **Создать ВМ**
2. Выбрать OS, ресурсы, диск, сеть
3. Создать

## CLI

```bash
fc compute instance create   --name app-server   --cores 2   --memory 4GiB   --disk-size 50GiB
```
