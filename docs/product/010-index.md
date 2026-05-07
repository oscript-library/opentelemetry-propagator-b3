---
title: B3 пропагатор для OpenTelemetry SDK
---

# B3 пропагатор для OpenTelemetry OneScript SDK

[![Quality Gate](https://sonar.openbsl.ru/api/project_badges/measure?project=opentelemetry-propagator-b3&metric=alert_status)](https://sonar.openbsl.ru/dashboard?id=opentelemetry-propagator-b3)
[![Coverage](https://sonar.openbsl.ru/api/project_badges/measure?project=opentelemetry-propagator-b3&metric=coverage)](https://sonar.openbsl.ru/component_measures?id=opentelemetry-propagator-b3&metric=coverage)
[![Bugs](https://sonar.openbsl.ru/api/project_badges/measure?project=opentelemetry-propagator-b3&metric=bugs)](https://sonar.openbsl.ru/project/issues?id=opentelemetry-propagator-b3&resolved=false&types=BUG)
[![Code Smells](https://sonar.openbsl.ru/api/project_badges/measure?project=opentelemetry-propagator-b3&metric=code_smells)](https://sonar.openbsl.ru/project/issues?id=opentelemetry-propagator-b3&resolved=false&types=CODE_SMELL)
[![Telegram](https://img.shields.io/badge/Telegram-чат-blue?logo=telegram)](https://t.me/autumn_winow)

## Что это такое

B3 (Zipkin) пропагатор для [OpenTelemetry SDK](https://github.com/nixel2007/opentelemetry)
на OneScript.

B3 — формат заголовков трассировки, изначально разработанный в Zipkin и широко используемый
в экосистеме микросервисов (Istio, Envoy, Spring Cloud Sleuth и другие).

### Почему отдельный пакет?

Согласно [спецификации OpenTelemetry Propagators Distribution](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/context/api-propagators.md#propagators-distribution),
официальный список пропагаторов **MUST be distributed as separate, optional packages**.
Этот пакет — отдельная поставка B3-пропагатора, чтобы основной SDK не нёс зависимостей
на не-W3C форматы.

## Установка

```sh
opm install opentelemetry-propagator-b3
```

## Быстрый старт

```bsl
#Использовать opentelemetry
#Использовать opentelemetry-propagator-b3

// По умолчанию single-header формат: b3: {trace}-{span}-{sampled}
Пропагатор = Новый ОтелB3Пропагатор();

// Multi-header формат: X-B3-TraceId, X-B3-SpanId, X-B3-Sampled
Пропагатор = Новый ОтелB3Пропагатор(ОтелФорматB3.Мульти());

// Внедрить контекст в исходящий запрос
Носитель = Новый Соответствие();
Пропагатор.Внедрить(ОтелКонтекст.Текущий(), Носитель);

// Извлечь контекст из входящего запроса
КонтекстВходящий = Пропагатор.Извлечь(Новый Соответствие(), ВходящиеЗаголовки);
```

## Поддерживаемые форматы

| Формат | Константа | Заголовки |
|--------|-----------|-----------|
| `single` (по умолчанию) | `ОтелФорматB3.Одиночный()` | `b3: {traceId}-{spanId}-{sampled}-{parentSpanId}` |
| `multi` | `ОтелФорматB3.Мульти()` | `X-B3-TraceId`, `X-B3-SpanId`, `X-B3-Sampled`, `X-B3-Flags` |

При извлечении контекста оба формата поддерживаются одновременно: `single-header (b3)` имеет
приоритет над `multi-header (X-B3-*)`.

## Требования совместимости

- OneScript `>= 1.0.0`
- OpenTelemetry SDK для OneScript `>= 1.0.0`

## API

Полная документация по публичному интерфейсу: [API Reference](/api/opentelemetry-propagator-b3/)

- [ОтелB3Пропагатор](/api/opentelemetry-propagator-b3/Классы/ОтелB3Пропагатор.md)
- [ОтелФорматB3](/api/opentelemetry-propagator-b3/Модули/ОтелФорматB3.md)
