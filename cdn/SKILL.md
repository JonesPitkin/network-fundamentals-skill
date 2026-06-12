---
name: cdn
description: "Объяснять CDN: edge caching, latency reduction, origin shielding, reliability и security implications для веб-сервисов и VPN control plane."
---

# CDN

## 1. Что это такое

`CDN` — это распределённая сеть edge-серверов, которая кэширует контент ближе к пользователю и помогает доставлять его быстрее, надёжнее и безопаснее. Cloudflare описывает CDN как способ ускорять доставку, уменьшать latency и повышать availability.

## 2. Зачем это нужно

- сокращать физическую дистанцию до пользователя;
- кэшировать статические ресурсы и снижать нагрузку на origin;
- повышать uptime за счёт распределённой инфраструктуры;
- добавлять edge security, включая certificate management и DDoS mitigation.

## 3. Как это связано с VPN-инфраструктурой

- CDN полезен для web-facing control plane, subscription pages и documentation portals;
- он не заменяет сам VPN transport, но укрепляет и ускоряет околовебовую инфраструктуру;
- при публикации панелей и pages нужно понимать разницу между edge path и origin path.

## 4. Как это связано с OpenWrt

- клиенты за OpenWrt часто ходят к CDN-protected services;
- диагностика должна учитывать anycast-like edge behavior и то, что ответ может идти не с origin;
- проблемы DNS или firewall на роутере могут проявляться как недоступность CDN edge.

## 5. Как это связано с Cloudflare

- Cloudflare — типичный CDN/edge layer в этой экосистеме;
- он добавляет caching, reliability, certificate handling и traffic filtering;
- важно различать response от edge и реальное состояние origin.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` могут публиковать web layers через Cloudflare;
- `sing-box` и `Podkop` взаимодействуют с CDN-hosted APIs и assets;
- `Nginx Proxy Manager` часто находится на origin side за CDN;
- CDN особенно полезен для статических web assets и публичных landing/subscription pages.

## 7. Типовые ошибки

- считать CDN заменой origin security;
- забывать, что CDN edge может кэшировать или менять observed behavior;
- диагностировать только origin IP, когда клиент реально ходит в edge;
- проксировать через CDN всё подряд без понимания protocol expectations.

## 8. Диагностика

1. Определить, идёт ли запрос в CDN edge или напрямую в origin.
2. Понять, что ломается: DNS, edge, origin, reverse proxy или app.
3. Проверить caching behavior и ожидания по freshness.
4. Различать performance issue и availability/security issue.
5. Проверить edge/origin boundary.

## 9. Практические примеры

- Публикация subscription page `Remnawave` через Cloudflare CDN.
- Разбор, почему static assets панели быстрые, а API тормозит на origin.
- Сравнение direct origin response и Cloudflare edge response.
- Объяснение, почему anycast edge делает latency/traceroute interpretation неочевидными.

## 10. Checklist для Codex

- Уточнить, используется ли CDN и какой именно.
- Разделить browser -> edge и edge -> origin.
- Проверить, должна ли сущность кэшироваться.
- Не путать CDN, reverse proxy и WAF в одну сущность.
- При необходимости перейти в [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md), [../https/SKILL.md](../https/SKILL.md) и [../tls/SKILL.md](../tls/SKILL.md).
