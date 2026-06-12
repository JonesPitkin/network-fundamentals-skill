---
name: http2-http3
description: "Объяснять HTTP/2, HTTP/3 и QUIC: multiplexing, latency, head-of-line blocking и их влияние на современные web-facing сервисы."
---

# HTTP/2, HTTP/3, QUIC

## 1. Что это такое

`HTTP/2` и `HTTP/3` — современные версии HTTP. MDN отмечает, что `HTTP/2` направлен на снижение latency и head-of-line blocking, а `HTTP/3` использует `QUIC` поверх `UDP` вместо `TCP`. `QUIC` — это multiplexed transport protocol, designed for quicker setup and lower latency.

## 2. Зачем это нужно

- уменьшать задержку и ускорять загрузку;
- улучшать multiplexing и работу нескольких streams;
- сокращать head-of-line blocking;
- повышать эффективность modern web publication.

## 3. Как это связано с VPN-инфраструктурой

- панели, dashboards и subscription pages часто публикуются как современные web-приложения;
- transport behavior `HTTP/2`/`HTTP/3` влияет на user experience вокруг control plane;
- QUIC/UDP path особенно важен там, где firewall или network policy иначе ведут себя по отношению к UDP.

## 4. Как это связано с OpenWrt

- OpenWrt firewall и path MTU могут влиять на `HTTP/3`/`QUIC` иначе, чем на TCP-based traffic;
- на роутере важно различать проблемы обычного HTTPS/TCP и проблемы QUIC over UDP;
- при сетевой диагностике browser может fallback между HTTP versions.

## 5. Как это связано с Cloudflare

- Cloudflare активно участвует в edge delivery modern web protocols;
- `HTTP/3` и `QUIC` особенно заметны на CDN/edge уровне;
- performance behavior panels and pages за Cloudflare может отличаться от plain origin path.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` имеют web-facing surfaces, где modern HTTP transport влияет на perceived performance;
- `sing-box` и `Podkop` часто используются в сетях с нестандартной UDP/TCP policy, что влияет на QUIC behavior;
- `Nginx Proxy Manager` и `NGINX` участвуют в публикации HTTP services, где важно понимать protocol differences.

## 7. Типовые ошибки

- считать `HTTP/3` просто “быстрым HTTPS” без понимания QUIC;
- игнорировать, что `HTTP/3` идёт поверх UDP;
- путать app-level performance issue и transport-level issue;
- забывать, что firewall policy для UDP может ломать QUIC path.

## 8. Диагностика

1. Проверить, какая версия HTTP реально используется.
2. Разделить TCP/TLS path и UDP/QUIC path.
3. Проверить firewall и middleboxes для UDP.
4. Проверить, не происходит ли fallback до HTTP/2 или HTTP/1.1.
5. Учитывать CDN/reverse proxy support for modern protocols.

## 9. Практические примеры

- Разбор, почему панель работает по HTTP/2, но HTTP/3 нестабилен.
- Объяснение разницы latency behavior между TCP/TLS и QUIC.
- Проверка OpenWrt-сети, где UDP policy ломает QUIC, но обычный HTTPS работает.
- Анализ performance differences через Cloudflare edge.

## 10. Checklist для Codex

- Уточнить, о каком уровне вопрос: HTTP version, QUIC transport или browser behavior.
- Проверить, участвует ли UDP path.
- Не путать TLS issue и QUIC/HTTP/3 issue.
- При необходимости перейти в [../tls/SKILL.md](../tls/SKILL.md), [../https/SKILL.md](../https/SKILL.md) и [../firewall/SKILL.md](../firewall/SKILL.md).
