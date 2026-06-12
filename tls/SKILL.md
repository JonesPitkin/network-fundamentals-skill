---
name: tls
description: "Объяснять TLS: handshake, сертификаты, encryption, integrity, authentication и их роль в безопасной публикации панелей, API, прокси и VPN-сервисов."
---

# TLS

## 1. Что это такое

`TLS` — это протокол для безопасной связи клиента и сервера через недоверенную сеть. MDN и Cloudflare описывают TLS как механизм, который даёт `encryption`, `integrity` и `authentication`. На вебе TLS чаще всего используется как основа для `HTTPS`.

## 2. Зачем это нужно

- защищать трафик от чтения и подмены;
- подтверждать подлинность сервера через сертификат;
- безопасно публиковать панели, API и subscription endpoints;
- снижать риск `MITM` и downgrade/stripping-сценариев.

## 3. Как это связано с VPN-инфраструктурой

- VPN-панели и control-plane endpoints обычно публикуются по TLS;
- даже если сам VPN transport не HTTP, рядом почти всегда есть web/API layer;
- выдача токенов, логинов, конфигов и dashboard-сессий без TLS создаёт лишний риск.

## 4. Как это связано с OpenWrt

- OpenWrt-роутер часто выступает клиентом к TLS-сервисам: dashboards, APIs, web portals;
- сетевые проблемы на роутере могут проявляться как `TLS handshake failed`;
- важно понимать, где TLS терминируется: на origin, reverse proxy или CDN edge.

## 5. Как это связано с Cloudflare

- Cloudflare использует TLS на edge и отдельно требует понимания origin-side TLS;
- при публикации панели через Cloudflare нужно различать browser-to-edge и edge-to-origin path;
- edge-сертификат не отменяет необходимость корректного origin security.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` публикуют web-facing panel/API surfaces;
- `sing-box` и `Podkop` зависят от корректного понимания TLS как части инфраструктуры вокруг сервисов и панелей;
- `Nginx Proxy Manager` часто используется как TLS termination point перед backend-сервисами;
- ошибки вокруг TLS чаще ломают control plane, а не сам VPN tunnel.

## 7. Типовые ошибки

- использовать устаревшие версии TLS;
- путать сертификат и сам протокол TLS;
- считать, что green lock автоматически означает безопасный origin;
- завершать TLS на одном слое и игнорировать exposure дальше до backend;
- смешивать DNS, TCP, TLS и HTTP в одну причину сбоя.

## 8. Диагностика

1. Проверить DNS и IP reachability.
2. Проверить TCP reachability до `443`.
3. Проверить certificate validity и hostname match.
4. Определить, где происходит TLS termination.
5. Проверить, не ломают ли path firewall, MTU или reverse proxy/CDN layer.

## 9. Практические примеры

- Публикация `3x-ui` за reverse proxy с валидным TLS.
- Защита `Remnawave` panel и API через TLS перед публикацией в Интернет.
- Разбор случая, когда OpenWrt видит IP и маршрут, но HTTPS/TLS handshake зависает.
- Объяснение, почему subscription page за Cloudflare требует корректного origin TLS.

## 10. Checklist для Codex

- Уточнить, речь о TLS как transport security или о полном HTTPS publication.
- Определить hops: client -> CDN -> reverse proxy -> origin.
- Проверить версии TLS и место termination.
- Не смешивать сертификат, DNS, HTTPS redirect и firewall policy.
- Для web publication при необходимости перейти в [../https/SKILL.md](../https/SKILL.md) и [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md).
