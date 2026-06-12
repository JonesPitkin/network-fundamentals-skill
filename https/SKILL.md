---
name: https
description: "Объяснять HTTPS: secure HTTP over TLS, redirects, HSTS, mixed content и безопасную публикацию web-панелей, API и subscription pages."
---

# HTTPS

## 1. Что это такое

`HTTPS` — это зашифрованная версия `HTTP`, которая использует `TLS` для защиты связи между клиентом и сервером. MDN определяет HTTPS как secure HTTP connection для безопасного обмена чувствительными данными.

## 2. Зачем это нужно

- защищать логины, токены, cookies и panel/API traffic;
- предотвращать подмену контента на пути;
- обеспечивать browser `secure context`;
- минимизировать риск `MITM` и SSL stripping.

## 3. Как это связано с VPN-инфраструктурой

- панели, dashboards, subscription pages и admin endpoints почти всегда web-facing;
- даже если VPN transport не HTTP, control plane часто работает через браузер и API;
- insecure HTTP для admin/public web-layer создаёт лишний риск утечки и подмены.

## 4. Как это связано с OpenWrt

- OpenWrt часто служит gateway для клиентов, которые ходят к HTTPS-сервисам;
- локальная публикация web-интерфейсов через роутер требует понимания redirect и TLS boundary;
- DNS, firewall и MTU-проблемы на роутере часто проявляются как "HTTPS не работает".

## 5. Как это связано с Cloudflare

- Cloudflare часто выступает HTTPS edge перед origin;
- при публикации через Cloudflare нужно понимать redirect chain и edge/origin split;
- edge certificate не решает проблему небезопасного origin path сам по себе.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` имеют web-facing control plane;
- `sing-box` и `Podkop` взаимодействуют с web panels, downloadable configs и documentation portals;
- `Nginx Proxy Manager` напрямую связан с практической HTTPS-публикацией backend-сервисов.

## 7. Типовые ошибки

- оставлять панель на plain HTTP;
- делать redirect без понимания HSTS и first-request risk;
- забывать про mixed content;
- путать "HTTPS на edge" и "безопасный origin";
- публиковать backend по HTTPS, но не ограничивать прямой доступ к нему.

## 8. Диагностика

1. Проверить, что происходит при запросе `http://`.
2. Проверить, открывается ли `https://` endpoint.
3. Проверить certificate validity и hostname.
4. Проверить mixed content и redirect chain.
5. Проверить связку `DNS -> TCP/443 -> TLS -> HTTP response`.

## 9. Практические примеры

- Перевод panel domain `3x-ui` с HTTP на HTTPS за reverse proxy.
- Публикация `Remnawave` subscription page по HTTPS за Cloudflare.
- Разбор mixed content после перевода панели на HTTPS.
- Сравнение прямого origin доступа и доступа через CDN/proxy chain.

## 10. Checklist для Codex

- Выяснить, что именно публикуется: panel, API, dashboard или subscription page.
- Проверить redirect с HTTP на HTTPS.
- Проверить, есть ли mixed content или insecure subresources.
- Разделить проблемы TLS, DNS, reverse proxy и firewall.
- При необходимости перейти в [../tls/SKILL.md](../tls/SKILL.md) и [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md).
