---
name: firewall
description: "Объяснять firewall: packet filtering, zones, exposure control и их роль в OpenWrt, Linux hosts, reverse proxy и VPN-публикации."
---

# Firewall

## 1. Что это такое

`Firewall` — это слой фильтрации и policy enforcement для сетевого трафика. В OpenWrt официальная документация выделяет firewall как отдельный конфигурационный слой для управления доступом между зонами и сервисами.

## 2. Зачем это нужно

- ограничивать поверхность атаки;
- разрешать только нужные входящие и исходящие потоки;
- разделять LAN/WAN/service zones;
- не допускать случайной публикации panel/API/backend ports.

## 3. Как это связано с VPN-инфраструктурой

- VPN-инфраструктура ломается и по безопасности, и по доступности, если firewall policy неточна;
- открытые admin ports, неверные forwards и слишком широкие allow rules создают лишний риск;
- firewall определяет, какие control-plane и data-plane paths реально достижимы.

## 4. Как это связано с OpenWrt

- это один из самых прямых разделов для OpenWrt, потому что роутер сам управляет traffic filtering;
- OpenWrt firewall нужен для WAN exposure, inter-zone policy и ограничения доступа к локальным сервисам;
- ошибки в OpenWrt firewall часто выглядят как "не работает panel/API/DNS/VPN".

## 5. Как это связано с Cloudflare

- Cloudflare не заменяет локальный firewall на origin;
- даже при публикации через edge, origin firewall должен ограничивать прямой доступ;
- firewall особенно важен, если origin IP достижим напрямую.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `Podkop` и `sing-box` тесно связаны с policy routing и traffic interception;
- `3x-ui` и `Remnawave` требуют аккуратного ограничения panel/API exposure;
- для `Nginx Proxy Manager` firewall помогает гарантировать, что backend доступен только через ожидаемый path.

## 7. Типовые ошибки

- открывать слишком много портов "на всякий случай";
- считать CDN или reverse proxy заменой firewall;
- разрешать прямой доступ к backend или panel port;
- не различать inbound publication и lateral access внутри сети;
- менять firewall и не перепроверять возвратный path.

## 8. Диагностика

1. Определить, какой трафик должен быть разрешён и между какими зонами.
2. Проверить, доступен ли сервис локально и недоступен ли только извне.
3. Проверить, не открыт ли origin в обход proxy/CDN.
4. Отдельно смотреть host firewall, router firewall и edge filtering.
5. Проверить expected path и unwanted direct path.

## 9. Практические примеры

- Ограничение доступа к `3x-ui` panel только через reverse proxy.
- Ограничение `Remnawave` origin так, чтобы публично работал только нужный web entrypoint.
- Разбор OpenWrt-кейса, где LAN видит сервис, а WAN нет из-за zone policy.
- Проверка, что backend за `Nginx Proxy Manager` не принимает прямые соединения из Интернета.

## 10. Checklist для Codex

- Определить, где именно firewall: host, OpenWrt router, cloud edge.
- Проверить expected path и unwanted direct path.
- Разделить exposure problem и application problem.
- Для OpenWrt явно проговорить zone-based thinking.
- Для Cloudflare и reverse proxy отдельно проверить direct-origin exposure.
- При необходимости перейти в [../linux-networking/SKILL.md](../linux-networking/SKILL.md) и [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md).
