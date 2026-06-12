---
name: linux-networking
description: "Объяснять Linux networking: interfaces, addresses, routes, sockets, listeners, reachability и host-side диагностику для VPN, OpenWrt-adjacent и proxy-published сервисов."
---

# Linux Networking

## 1. Что это такое

`Linux networking` — это host-side сетевая модель Linux: интерфейсы, адреса, маршруты, сокеты, listening services и прикладная диагностика. Для VPN-инфраструктуры это базовая операционная почва, на которой живут панели, reverse proxy, agents и вспомогательные сервисы.

## 2. Зачем это нужно

- понимать, как сервис реально слушает трафик;
- проверять адреса, маршруты и reachability на сервере;
- локализовать проблемы между app, host network, firewall и upstream;
- безопасно публиковать сервисы и корректно ограничивать их listening scope.

## 3. Как это связано с VPN-инфраструктурой

- почти все панели и вспомогательные сервисы VPN-стека работают на Linux-хостах;
- без понимания interfaces, bind addresses, routes и sockets сложно диагностировать `3x-ui`, `Remnawave`, `NGINX` или subscription pages;
- это базовый слой для host-side части VPN control plane.

## 4. Как это связано с OpenWrt

- OpenWrt тоже Linux-based, поэтому часть мышления похожа: интерфейсы, адреса, маршруты, sockets, firewall;
- OpenWrt даёт router-first perspective, а обычный Linux server — host/application-first perspective;
- полезно отличать проблему на роутере от проблемы на Linux origin.

## 5. Как это связано с Cloudflare

- при публикации через Cloudflare origin всё равно остаётся Linux-хостом с interfaces, listeners и routes;
- edge layer не отменяет необходимость понимать bind address, local reachability и host firewall;
- диагностика "Cloudflare не работает" часто упирается в Linux origin state.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` — типичные Linux-hosted panels;
- `sing-box` часто запускается как Linux service и требует понимания interfaces, routes и listeners;
- `Podkop` близок к OpenWrt/Linux networking как operational среде;
- `Nginx Proxy Manager` и обычный `NGINX` зависят от bind/listen/upstream reachability.

## 7. Типовые ошибки

- смотреть только на приложение и не проверять bind address;
- путать `127.0.0.1`, `0.0.0.0`, private LAN address и public WAN address;
- считать, что listening socket гарантирует внешнюю доступность;
- менять routing/firewall и не перепроверять путь обратно;
- искать проблему в Cloudflare или proxy, когда origin process не слушает нужный port.

## 8. Диагностика

1. Проверить interface state, IP address и route table.
2. Проверить listen sockets и bind scope.
3. Проверить reachability локально и снаружи.
4. Проверить связку `DNS -> TCP/UDP -> app listener`.
5. Различать проблему app, host network, firewall и external edge.

## 9. Практические примеры

- Диагностика `3x-ui`, который слушает только `127.0.0.1`.
- Проверка `Remnawave` panel за `NGINX`, когда upstream недоступен по локальному адресу.
- Разбор, почему Cloudflare edge не достукивается до Linux origin.
- Проверка `sing-box` service после изменения interfaces или policy routes.

## 10. Checklist для Codex

- Проверить interface state, IP addresses и routes.
- Проверить `listen`/`bind` scope процесса.
- Разделить host-side issue и edge-side issue.
- Не путать local success с public reachability.
- При необходимости перейти в [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md), [../firewall/SKILL.md](../firewall/SKILL.md) и [../https/SKILL.md](../https/SKILL.md).
