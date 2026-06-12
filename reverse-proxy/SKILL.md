---
name: reverse-proxy
description: "Объяснять reverse proxy: request forwarding, upstream abstraction, header passing, buffering и публикацию сервисов за NGINX или Nginx Proxy Manager."
---

# Reverse Proxy

## 1. Что это такое

`Reverse proxy` принимает клиентский запрос, передаёт его на upstream server и возвращает ответ клиенту. Официальная документация NGINX описывает это как базовую proxy-конфигурацию для передачи запросов, модификации request headers и управления buffering.

## 2. Зачем это нужно

- публиковать внутренние сервисы через один внешний вход;
- скрывать origin topology;
- централизовать TLS termination и redirects;
- маршрутизировать трафик на разные upstream services.

## 3. Как это связано с VPN-инфраструктурой

- VPN control plane часто публикуется через reverse proxy;
- это касается panel UI, subscription pages, API endpoints и dashboards;
- reverse proxy становится boundary между Интернетом и внутренними сервисами.

## 4. Как это связано с OpenWrt

- OpenWrt может быть gateway перед reverse-proxied сервисами;
- на edge важно различать: проблема в маршруте/port forward или в самом reverse proxy;
- firewall на роутере влияет на достижимость proxy endpoint и backend.

## 5. Как это связано с Cloudflare

- при публикации через Cloudflare reverse proxy часто находится на origin side;
- CDN и reverse proxy — разные слои: edge delivery и origin request handling;
- ошибки появляются на границе `Cloudflare -> NGINX/NPM -> upstream`.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` часто публикуются за `NGINX` или `Nginx Proxy Manager`;
- `sing-box` и `Podkop` взаимодействуют с reverse-proxied control-plane surfaces;
- reverse proxy помогает скрыть backend ports и аккуратно завершать HTTPS.

## 7. Типовые ошибки

- публиковать backend напрямую мимо proxy;
- путать reverse proxy с CDN;
- ломать upstream headers или request scheme;
- забывать, что buffering и forwarding меняют app behavior;
- не понимать, где заканчивается TLS и начинается upstream plain HTTP.

## 8. Диагностика

1. Проверить reachability до reverse proxy.
2. Проверить, отвечает ли upstream без proxy.
3. Проверить host/path routing.
4. Проверить headers и схему между слоями.
5. Проверить, не в DNS/firewall/CDN ли root cause.

## 9. Практические примеры

- Публикация `3x-ui` panel за `Nginx Proxy Manager`.
- Публикация `Remnawave` web layer за `NGINX`.
- Разбор `502/504`, когда backend не слушает ожидаемый port.
- Сравнение прямого доступа к backend и доступа через Cloudflare + reverse proxy.

## 10. Checklist для Codex

- Определить, есть ли chain `client -> CDN -> reverse proxy -> app`.
- Уточнить upstream scheme, port и host routing.
- Не смешивать reverse proxy, TLS и firewall в одну причину.
- Для Nginx Proxy Manager проверить, не открыт ли backend мимо proxy.
- При необходимости перейти в [../https/SKILL.md](../https/SKILL.md), [../tls/SKILL.md](../tls/SKILL.md) и [../firewall/SKILL.md](../firewall/SKILL.md).
