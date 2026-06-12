---
name: load-balancing
description: "Объяснять балансировку нагрузки: traffic distribution, failover, upstream groups и роль load balancing в availability, scalability и secure publication."
---

# Load Balancing

## 1. Что это такое

`Load balancing` — это распределение трафика между несколькими backend instances для повышения availability, scalability и resilience. NGINX прямо описывает load balancing как технику распределения трафика между application servers для throughput, reduced latency и fault tolerance.

## 2. Зачем это нужно

- избегать перегрузки одного backend;
- повышать отказоустойчивость;
- масштабировать приложения и панели;
- улучшать availability для публичных web/API endpoints.

## 3. Как это связано с VPN-инфраструктурой

- control plane вокруг VPN может требовать балансировки web/API layers;
- subscription pages, dashboards и reverse-proxied endpoints выигрывают от failover;
- load balancing особенно полезен для публичной публикации там, где важны uptime и мягкое масштабирование.

## 4. Как это связано с OpenWrt

- OpenWrt может быть клиентским edge до load-balanced services;
- для сетевой диагностики полезно понимать, что разные запросы могут попадать на разные backend;
- multi-WAN thinking и service availability на роутере conceptually близки к вопросам distribution/failover, хотя не тождественны.

## 5. Как это связано с Cloudflare

- Cloudflare edge delivery и distributed infrastructure тесно связаны с resilience concepts;
- Cloudflare materials прямо связывают CDN reliability с traffic distribution и failover;
- важно различать anycast edge distribution и application-level load balancing.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` могут расти до нескольких web-facing components;
- `sing-box` и `Podkop` чаще упираются в reachability и path, но соседняя инфраструктура dashboards/APIs может использовать LB;
- `Nginx Proxy Manager` и `NGINX` часто выступают точкой, где upstream balancing настраивается practically.

## 7. Типовые ошибки

- путать load balancing и anycast;
- ожидать session stickiness без явной конфигурации;
- балансировать сервис, backend которого не готов к нескольким instances;
- забывать, что health and failover logic влияют на observed behavior.

## 8. Диагностика

1. Проверить, один ли backend отвечает или их несколько.
2. Уточнить, есть ли sticky behavior.
3. Проверить failover expectations и health assumptions.
4. Разделить edge distribution и app-level balancing.
5. Проверить, не в reverse proxy ли root cause.

## 9. Практические примеры

- Балансировка нескольких backend web instances через `NGINX`.
- Разбор, почему часть запросов к одной панели даёт разный результат.
- Объяснение разницы между Cloudflare anycast edge и NGINX upstream load balancing.
- Проверка failover path при отказе одного origin.

## 10. Checklist для Codex

- Уточнить, это anycast/CDN distribution или app-level load balancing.
- Определить, есть ли upstream group и failover.
- Проверить необходимость session affinity.
- При необходимости перейти в [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md), [../cdn/SKILL.md](../cdn/SKILL.md) и [../anycast/SKILL.md](../anycast/SKILL.md).
