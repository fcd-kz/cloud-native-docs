# Справочник API

Это руководство содержит введение в API Media Processing Service (MPS) и описание того, как использовать их для запуска и управления задачами обработки медиа.

## Обзор

Media Processing Service предоставляет полный набор API для операций медиапроцессинга. Все API MPS соответствуют спецификации OpenAPI 3.0 и поддерживают RESTful-вызовы.

**Базовый URL API:** `mps.intl.tencentcloudapi.com`

Для операций, чувствительных к задержкам, вы можете указать региональный endpoint (например, `mps.ap-guangzhou.tencentcloudapi.com` для Гуанчжоу).

## Категории API

### API запуска задач обработки

Эти API используются для запуска задач обработки медиа:

| Название API | Возможность | Лимит запросов |
|----------|---------|-----------|
| **ProcessMedia** | Запуск одиночной задачи обработки медиа | 100 req/sec |
| **BatchProcessMedia** | Запуск пакетной обработки из нескольких URL | 20 req/sec |
| **ProcessLiveStream** | Запуск задачи обработки live-потока | 100 req/sec |
| **ProcessImage** | Запуск задачи обработки изображений | 20 req/sec |
| **EditMedia** | Редактирование видео | 20 req/sec |
| **DescribeMediaMetaData** | Получение метаданных медиа | 20 req/sec |
| **ExtractBlindWatermark** | Извлечение цифрового водяного знака из видео | 20 req/sec |

### API управления задачами

Эти API используются для запроса и управления задачами обработки медиа:

| Название API | Возможность | Лимит запросов |
|----------|---------|-----------|
| **DescribeTaskDetail** | Запрос деталей задачи | 100 req/sec |
| **DescribeTasks** | Получение списка задач | 100 req/sec |
| **DescribeBatchTaskDetail** | Запрос деталей пакетной задачи | 20 req/sec |
| **ManageTask** | Управление/завершение задачи | 20 req/sec |
| **DescribeImageTaskDetail** | Запрос деталей задачи обработки изображений | 20 req/sec |

### API управления шаблонами

Эти API управляют шаблонами обработки:

- **Шаблоны транскодирования**: CreateTranscodeTemplate, DeleteTranscodeTemplate, DescribeTranscodeTemplates, ModifyTranscodeTemplate
- **Шаблоны адаптивного битрейта**: CreateAdaptiveDynamicStreamingTemplate, DeleteAdaptiveDynamicStreamingTemplate, DescribeAdaptiveDynamicStreamingTemplates, ModifyAdaptiveDynamicStreamingTemplate
- **Шаблоны водяных знаков**: CreateWatermarkTemplate, DeleteWatermarkTemplate, DescribeWatermarkTemplates, ModifyWatermarkTemplate
- **Шаблоны скриншотов**: CreateSnapshotByTimeOffsetTemplate, CreateSampleSnapshotTemplate, CreateImageSpriteTemplate, CreateAnimatedGraphicsTemplate и варианты delete/describe/modify
- **Шаблоны Media AI**: CreateSmartSubtitleTemplate, CreateSmartEraseTemplate, CreateContentReviewTemplate, CreateAIAnalysisTemplate, CreateAIRecognitionTemplate и варианты
- **Шаблоны контроля качества**: CreateQualityControlTemplate, DeleteQualityControlTemplate, DescribeQualityControlTemplates, ModifyQualityControlTemplate
- **Шаблоны записи live**: CreateLiveRecordTemplate, DeleteLiveRecordTemplate, DescribeLiveRecordTemplates, ModifyLiveRecordTemplate

### API оркестраций / workflow

Эти API управляют автоматизированными workflow обработки:

| Название API | Возможность | Лимит запросов |
|----------|---------|-----------|
| **CreateSchedule** | Создание схемы оркестрации (scheme) | 20 req/sec |
| **CreateWorkflow** | Создание workflow | 200 req/sec |
| **DeleteSchedule** | Удаление схемы | 20 req/sec |
| **DeleteWorkflow** | Удаление workflow | 20 req/sec |
| **DescribeSchedules** | Запрос схем | 20 req/sec |
| **DescribeWorkflows** | Получение списка workflow | 20 req/sec |
| **EnableSchedule** | Включение авто-триггера схемы | 20 req/sec |
| **EnableWorkflow** | Включение workflow | 20 req/sec |
| **DisableSchedule** | Отключение схемы | 20 req/sec |
| **DisableWorkflow** | Отключение workflow | 20 req/sec |

### API парсинга уведомлений

| Название API | Возможность | Лимит запросов |
|----------|---------|-----------|
| **ParseNotification** | Парсинг уведомлений по offline-задачам | 20 req/sec |
| **ParseLiveStreamProcessNotification** | Парсинг уведомлений по задачам live-потоков | 20 req/sec |

## Начало работы с API ProcessMedia

### Обзор

API **ProcessMedia** используется для запуска задачи обработки для видео по URL или медиафайлов в Cloud Object Storage (COS).

Поддерживаемые возможности:
- Транскодирование аудио/видео (стандартное, TSC)
- Улучшение аудио/видео
- Добавление видимого водяного знака
- Добавление цифрового водяного знака
- Адаптивный битрейт-стриминг
- Конвертация видео в GIF
- Скриншот по времени
- Выборочные скриншоты
- Генерация image sprite
- Проверка качества медиа
- Генерация и перевод умных субтитров
- Умное стирание контента (водяные знаки, субтитры, приватность)
- Умная модерация контента (порнография, чувствительная информация)
- Умный анализ контента (теги, классификация, обложки, теги кадров, хайлайты)
- Умное распознавание контента (лица, текст, речь, объекты)

### Параметры запроса

**Обязательные параметры:**
- **Action**: String — значение: `ProcessMedia`
- **Version**: String — значение: `2019-06-12`
- **InputInfo**: MediaInputInfo — информация о файле для обработки

**Необязательные параметры:**
- **OutputStorage**: TaskOutputStorage — целевое хранилище для выходных файлов
- **OutputDir**: String — путь выходной директории (должен начинаться и заканчиваться на `/`)
- **MediaProcessTask**: MediaProcessTaskInput — параметры обработки медиа
- **AiContentReviewTask**: AiContentReviewTaskInput — параметры модерации контента
- **AiAnalysisTask**: AiAnalysisTaskInput — параметры анализа контента
- **AiRecognitionTask**: AiRecognitionTaskInput — параметры распознавания контента
- **AiQualityControlTask**: AiQualityControlTaskInput — параметры проверки качества
- **SmartSubtitlesTask**: SmartSubtitlesTaskInput — параметры умных субтитров
- **ScheduleId**: Integer — ID оркестрации для выполнения workflow
- **TaskNotifyConfig**: TaskNotifyConfig — настройки уведомлений о событиях
- **TasksPriority**: Integer — приоритет задачи (-10 до 10, по умолчанию: 0)
- **SessionContext**: String — сквозной контекст (до 1000 символов)
- **ResourceId**: String — ID ресурса для ресурсных операций
- **SkipMateData**: Integer — пропустить получение метаданных (0: нет, 1: да)

### Параметры ответа

- **TaskId**: String — уникальный идентификатор задачи обработки
- **RequestId**: String — уникальный ID запроса для поиска проблем

### Пример 1: Запуск задачи транскодирования

```json
{
  "InputInfo": {
    "Type": "COS",
    "CosInputInfo": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-chongqing",
      "Object": "movie201907WildAnimal.mov"
    }
  },
  "OutputStorage": {
    "Type": "COS",
    "CosOutputStorage": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-chongqing"
    }
  },
  "OutputDir": "output/",
  "MediaProcessTask": {
    "TranscodeTaskSet": [
      { "Definition": 20 },
      { "Definition": 30 },
      { "Definition": 40 }
    ]
  }
}


**Ответ:**
```json
{
  "Response": {
    "TaskId": "125xxx65-procedurev2-bffb15f07530b57bc1aabb01fac74bca",
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```

### Пример 2: Запуск задачи адаптивного битрейт-стриминга

```json
{
  "InputInfo": {
    "Type": "COS",
    "CosInputInfo": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-shanghai",
      "Object": "video/lego-city-vehicles.mp4"
    }
  },
  "OutputDir": "share/output/",
  "MediaProcessTask": {
    "AdaptiveDynamicStreamingTaskSet": [
      {
        "Definition": 10,
        "OutputObjectPath": "inputName-adaptiveDynamicStreaming.format",
        "SubStreamObjectName": "inputName-adaptiveDynamicStreaming-{definition}-{subStreamNumber}.format",
        "SegmentObjectName": "inputName-adaptiveDynamicStreaming-{definition}-{subStreamNumber}-{segmentNumber}.format"
      }
    ]
  }
}
```

### Пример 3: Запуск задачи проверки качества медиа

```json
{
  "InputInfo": {
    "Type": "COS",
    "CosInputInfo": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-shanghai",
      "Object": "image/lenna.jpeg"
    }
  },
  "OutputStorage": {
    "Type": "COS",
    "CosOutputStorage": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-shanghai"
    }
  },
  "OutputDir": "datashare/",
  "AiQualityControlTask": {
    "Definition": 30
  }
}
```

**Ответ:**
```json
{
  "Response": {
    "TaskId": "2600007696-WorkflowTask-67771a50b24d08baaf6165da23461e36tt7",
    "RequestId": "4a72e698-ec27-4fc1-8e17-c1cbfce1a4a9"
  }
}
```

## Запрос статуса задачи

### DescribeTaskDetail API

Используйте этот API, чтобы запросить детали и статус завершённой или выполняющейся задачи.

**Параметры запроса:**

- **TaskId**: String (обязательно) — Task ID для запроса

**Ответ:**

Возвращает подробную информацию, включая:
- Статус задачи (WAITING, PROCESSING, FINISH)
- Детали подзадач
- Данные входа (путь, размер, битрейт, длительность / file path, size, bitrate, duration)
- Данные выхода (расположение, разрешение, коде / file location, resolution, codec)
- Прогресс обработки и тайминги

### Пример запроса

```json
{
  "TaskId": "24000089-WorkflowTask-0723542d0c164c958ba116874fa9b0c4"
}
```

**Ответ:**
```json
{
  "Response": {
    "TaskId": "24000089-WorkflowTask-0723542d0c164c958ba116874fa9b0c4",
    "Status": "FINISH",
    "TaskType": "WorkflowTask",
    "CreateTime": "2025-05-16T07:44:26Z",
    "FinishTime": "2025-05-16T07:44:30Z",
    "RequestId": "147e6b46-efeb-48cf-9186-b195b2bf4f9d"
  }
}
```

## Управление задачами

### ManageTask API

Используйте этот API для управления задачами в очереди или в процессе выполнения.

**Параметры запроса:**

- **TaskId**: String (обязательно) — Task ID 
- **OperationType**: String (обязательно) — тип операции
  - `Abort`: завершить задачу

**Ограничения:**

- Для задач обработки live-потока: можно завершать задачи со статусом WAITING или PROCESSING
- Для остальных типов задач: можно завершать только задачи со статусом WAITING

### Пример: завершить задачу

```json
{
  "OperationType": "Abort",
  "TaskId": "2459149217-procedure-live-xxx51da009t0"
}
```

## Batch обработка

### BatchProcessMedia API

Используйте этот API, чтобы обработать несколько видео по URL в одном запросе.

**Лимит:**  20 запросов в секунду

**Возможности:**
- Генерация умных субтитров с распознаванием речи и переводом
- Вход из нескольких источников URL
- Пакетный вывод в одну локацию

### Пример: пакетная генерация субтитров

```json
{
  "InputInfo": [
    {
      "Type": "URL",
      "UrlInputInfo": {
        "Url": "https://test-xxx-125xxxxx.cos.ap-xxxxx.myqcloud.com/processmedia52.mp4"
      }
    }
  ],
  "OutputStorage": {
    "Type": "COS",
    "CosOutputStorage": {
      "Bucket": "test-xxxx-125xxxxx",
      "Region": "ap-xxxxx"
    }
  },
  "OutputDir": "output/",
  "SmartSubtitlesTask": {
    "RawParameter": {
      "SubtitleType": 2,
      "VideoSrcLanguage": "zh",
      "SubtitleFormat": "vtt",
      "TranslateSwitch": "ON",
      "TranslateDstLanguage": "en"
    }
  },
  "TaskNotifyConfig": {
    "NotifyType": "URL",
    "NotifyUrl": "http://xxxx.com/v2/pushmps?token=73YcsZyP"
  }
}
```

**Ответ:**
```json
{
  "Response": {
    "TaskId": "24000030-BatchTask-e6fefa34fc497449c1a043b9a594c7det20",
    "RequestId": "b30891cd-cdc7-47db-94d3-4dbb85641dad"
  }
}
```

## Обработка live-потоков

### ProcessLiveStream API

Используйте этот API для запуска обработки live-потоков в реальном времени.

**Лимит:** 100 запросов в секунду

**Поддерживаемые возможности:**
- Умная модерация (порнография, чувствительная информация)
- Интеллектуальная идентификация (лица, объекты, текст, речь, перевод)
- Интеллектуальный анализ (сегментация новостей, realtime-фичи)
- Проверка качества (диагностика формата, детекция контента, no-reference скоринг)
- Запись live-потока

## Ресурсы для разработчиков

### SDKs

TencentCloud API 3.0 предоставляет SDK для нескольких языков программирования:

- Tencent Cloud SDK 3.0 для Python
- Tencent Cloud SDK 3.0 для Java
- Tencent Cloud SDK 3.0 для PHP
- Tencent Cloud SDK 3.0 для Go
- Tencent Cloud SDK 3.0 для Node.js
- Tencent Cloud SDK 3.0 для .NET
- Tencent Cloud SDK 3.0 для C++

### Command Line Interface

- Tencent Cloud CLI 3.0

### API Explorer

Используйте инструмент [API Explorer](https://cloud.tencent.com/api/explorer), чтобы:
- вызывать API онлайн
- генерировать код SDK
- тестировать аутентификацию и подписи
-смотреть примеры запросов и ответов

## Частые коды ошибок

|  Код ошибки | Описание |
|-----------|-------------|
| `FailedOperation.InvalidMpsUser` | Ошибка операции: неавторизованный пользователь MPSr |
| `InternalError` | Внутренняя ошибка сервиса |
| `InvalidParameterValue` | Некорректное значение параметра  |
| `InvalidParameterValue.Limit` | Некорректный параметр limit |
| `InvalidParameter` | Некорректный формат параметра |
| `UnauthorizedOperation` | Пользователь не авторизован |

## Best Practices

1. Используйте шаблоны: создавайте и переиспользуйте шаблоны для стабильных параметров

2. Пакетная обработка: используйте BatchProcessMedia для эффективной обработки множества файлов

3. Уведомления о событиях: настраивайте TaskNotifyConfig для получения уведомлений о завершении

4. Обработка ошибок: реализуйте корректную обработку ошибок для упавших задач

5. Управление ресурсами: используйте ResourceId для трекинга и распределения затрат

6. Ограничения по rate limit: соблюдайте лимиты и используйте backoff

7. Оркестрации: используйте workflow для сложных многошаговых пайплайнов

## Связанные темы

- [Руководство по началу работы](/quickstart/quickstart.md)
- [Задачи транскодирования](/operations/transcoding-tasks.md)
- [Улучшение видео](/operations/enhancement.md)
- [Запись прямых трансляций](/operations/live-recording.md)
