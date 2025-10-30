# Быстрый старт

## Создание ВМ через портал

1. Перейдите в **Compute**
2. Нажмите **Создать виртуальную машину**
3. Выберите:
   - образ OS
   - vCPU / RAM
   - диск
   - сеть
4. Создайте ВМ

## CLI

```bash
fc compute instance create   --name my-vm   --cores 2   --memory 4GiB
```

## Подключение к ВМ

```bash
ssh ubuntu@<IP>
```
