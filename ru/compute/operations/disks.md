# Работа с дисками

## Подключить диск

```bash
fc compute disk attach   --disk-id <ID>   --instance-id <VM_ID>
```

## Отсоединить диск

```bash
fc compute disk detach --disk-id <ID>
```

## Создать снимок

```bash
fc compute snapshot create --disk-id <ID>
```
