# opentelemetry-propagator-b3

B3 (Zipkin) пропагатор для [OpenTelemetry SDK](https://github.com/nixel2007/opentelemetry) на OneScript.

Согласно [спецификации OpenTelemetry Propagators Distribution](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/context/api-propagators.md#propagators-distribution), официальный список пропагаторов **MUST be distributed as separate, optional packages**. Этот пакет — отдельная поставка B3-пропагатора, чтобы основной SDK не нёс зависимостей на не-W3C форматы.

## Установка

```sh
opm install opentelemetry-propagator-b3
```

## Использование

```bsl
#Использовать opentelemetry
#Использовать opentelemetry-propagator-b3

// По умолчанию single-header формат: b3: {trace}-{span}-{sampled}
Пропагатор = Новый ОтелB3Пропагатор();

// Multi-header формат: X-B3-TraceId, X-B3-SpanId, X-B3-Sampled
Пропагатор = Новый ОтелB3Пропагатор(ОтелФорматB3.Мульти());

Носитель = Новый Соответствие();
Пропагатор.Внедрить(ОтелКонтекст.Текущий(), Носитель);

КонтекстВходящий = Пропагатор.Извлечь(Новый Соответствие(), ВходящиеЗаголовки);
```

## Поддерживаемые форматы

| Формат | Заголовки |
|---|---|
| `single` (по умолчанию) | `b3: {traceId}-{spanId}-{sampled}-{parentSpanId}` |
| `multi` | `X-B3-TraceId`, `X-B3-SpanId`, `X-B3-Sampled`, `X-B3-Flags` |

## Совместимость

Требуется OpenTelemetry SDK для OneScript версии `>= 1.0.0`.

## Лицензия

[MIT](LICENSE.md) © 2026 Nikita Fedkin
