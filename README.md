# network-fundamentals-skill

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status: Publish Ready](https://img.shields.io/badge/status-publish--ready-2ea44f)

`network-fundamentals-skill` — standalone Codex skill-репозиторий с фундаментальной базой знаний по компьютерным сетям на русском языке. Репозиторий нужен как общий сетевой entrypoint для объяснения теории, пошаговой диагностики и повседневной эксплуатации Linux, OpenWrt и VPN-инфраструктуры.

## Описание проекта

Репозиторий покрывает:

- модель `OSI` и диагностическое разложение проблем по слоям;
- практический стек `TCP/IP`;
- `TCP`, `UDP` и транспортное поведение;
- `DNS`, типы resolver/server roles и типовые инциденты;
- `ports`, sockets и transport demultiplexing;
- `NAT`, `PAT` и `CGNAT`;
- `MTU`, `MSS`, `PMTUD` и фрагментацию;
- `gateway`, `routing`, `IPv4` и `IPv6`;
- `TLS`, `HTTPS`, `CDN`, `reverse proxy`, `firewall` и `linux networking` как базовый слой для VPN-публикации, edge-защиты и web-facing control plane.
- `anycast`, `BGP`, `DNS security`, `mTLS`, `HTTP/2`, `HTTP/3`, `QUIC` и `load balancing` как следующий фундамент для Cloudflare, Nginx Proxy Manager, OpenWrt и современных VPN-репозиториев.

## Quick Start

1. Начать с [SKILL.md](./SKILL.md) как с главного repository entrypoint.
2. Если проблема еще не локализована, перейти в [osi-model/SKILL.md](./osi-model/SKILL.md).
3. Если вопрос про реальную сетевую механику, затем открыть [tcp-ip/SKILL.md](./tcp-ip/SKILL.md).
4. Для адресации, маршрута и выхода в Интернет использовать `ipv4`, `ipv6`, `routing`, `gateway`.
5. Для приложений и отказов поверх IP использовать `dns`, `tcp-vs-udp`, `ports`, `nat`, `cgnat`, `mtu`.
6. Для безопасной публикации сервисов и панелей использовать `tls`, `https`, `cdn`, `reverse-proxy`, `firewall`, `linux-networking`.
7. Для edge-маршрутизации, secure DNS, modern web transport и high-availability publication использовать `anycast`, `bgp`, `dns-security`, `mtls`, `http2-http3`, `load-balancing`.

## Карта разделов

| Раздел | Назначение |
| --- | --- |
| [SKILL.md](./SKILL.md) | Главный entrypoint и роутер по сетевым темам |
| [SKILL_INDEX.md](./SKILL_INDEX.md) | Полный список skills и их ролей |
| [VERSION_MATRIX.md](./VERSION_MATRIX.md) | Матрица версий, стандартов и совместимости |
| [CHANGELOG.md](./CHANGELOG.md) | История publish-ready изменений |
| [CONTRIBUTING.md](./CONTRIBUTING.md) | Правила внесения изменений |
| [RELEASE_v1.0.0.md](./RELEASE_v1.0.0.md) | Описание первого publish-ready релиза |
| [references/](./references/) | Корневые reference-материалы по репозиторию |
| [osi-model/](./osi-model/) | Диагностика по слоям |
| [tcp-ip/](./tcp-ip/) | Реальная интернет-стековая модель |
| [tcp-vs-udp/](./tcp-vs-udp/) | Сравнение транспортов |
| [dns/](./dns/) | Разрешение имен и DNS-диагностика |
| [ports/](./ports/) | Порты, сокеты и listen/connect behavior |
| [nat/](./nat/) | Address translation и service publishing |
| [cgnat/](./cgnat/) | Операторский NAT и его ограничения |
| [mtu/](./mtu/) | Размер пакета, MSS и PMTUD |
| [gateway/](./gateway/) | Default gateway и next hop |
| [routing/](./routing/) | Выбор пути и route lookup |
| [ipv4/](./ipv4/) | IPv4 адресация и private/public ranges |
| [ipv6/](./ipv6/) | IPv6 адресация, NDP, SLAAC и PMTUD |
| [tls/](./tls/) | TLS, сертификаты и secure transport |
| [https/](./https/) | HTTPS, redirects и безопасная web-публикация |
| [cdn/](./cdn/) | CDN, edge cache, latency и reliability |
| [reverse-proxy/](./reverse-proxy/) | Reverse proxy, upstream и публикация приложений |
| [firewall/](./firewall/) | Firewall policy, exposure control и OpenWrt firewall |
| [linux-networking/](./linux-networking/) | Linux interfaces, routes, listeners и host-side network diagnostics |
| [anycast/](./anycast/) | Anycast routing, DNS edge и Cloudflare delivery model |
| [bgp/](./bgp/) | BGP и интернет-маршрутизация между автономными системами |
| [dns-security/](./dns-security/) | DNSSEC, DoH, DoT и secure DNS |
| [mtls/](./mtls/) | Mutual TLS и двусторонняя аутентификация |
| [http2-http3/](./http2-http3/) | HTTP/2, HTTP/3 и QUIC |
| [load-balancing/](./load-balancing/) | Балансировка нагрузки и отказоустойчивость |

## Структура проекта

```text
network-fundamentals-skill/
├── README.md
├── SKILL.md
├── SKILL_INDEX.md
├── VERSION_MATRIX.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── RELEASE_v1.0.0.md
├── LICENSE
├── AUDIT.md
├── QUALITY_REPORT.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── sources.md
│   ├── repository-map.md
│   └── standalone-compatibility.md
├── osi-model/
├── tcp-ip/
├── tcp-vs-udp/
├── dns/
├── ports/
├── nat/
├── cgnat/
├── mtu/
├── gateway/
├── routing/
├── ipv4/
├── ipv6/
├── tls/
├── https/
├── cdn/
├── reverse-proxy/
├── firewall/
├── linux-networking/
├── anycast/
├── bgp/
├── dns-security/
├── mtls/
├── http2-http3/
└── load-balancing/
```

## Порядок изучения

1. [osi-model](./osi-model/SKILL.md)
2. [tcp-ip](./tcp-ip/SKILL.md)
3. [ipv4](./ipv4/SKILL.md)
4. [ipv6](./ipv6/SKILL.md)
5. [routing](./routing/SKILL.md)
6. [gateway](./gateway/SKILL.md)
7. [tcp-vs-udp](./tcp-vs-udp/SKILL.md)
8. [ports](./ports/SKILL.md)
9. [dns](./dns/SKILL.md)
10. [nat](./nat/SKILL.md)
11. [cgnat](./cgnat/SKILL.md)
12. [mtu](./mtu/SKILL.md)
13. [linux-networking](./linux-networking/SKILL.md)
14. [firewall](./firewall/SKILL.md)
15. [tls](./tls/SKILL.md)
16. [https](./https/SKILL.md)
17. [reverse-proxy](./reverse-proxy/SKILL.md)
18. [cdn](./cdn/SKILL.md)
19. [anycast](./anycast/SKILL.md)
20. [bgp](./bgp/SKILL.md)
21. [dns-security](./dns-security/SKILL.md)
22. [mtls](./mtls/SKILL.md)
23. [http2-http3](./http2-http3/SKILL.md)
24. [load-balancing](./load-balancing/SKILL.md)

## Источники

Основные источники знаний:

- `RFC Editor`
- `Cloudflare Learning Center`
- `Cisco Networking Academy`
- `OpenWrt Networking Docs`
- `MDN Networking`

Полный список ссылок: [references/sources.md](./references/sources.md)

## Связанные репозитории

- [sing-box-skills](https://github.com/JonesPitkin/sing-box-skills) — standalone skill-репозиторий по `sing-box`.
- [3x-ui-skills](https://github.com/JonesPitkin/3x-ui-skills) — standalone skill-репозиторий по `3x-ui`.
- [remnawave-skills](https://github.com/JonesPitkin/remnawave-skills) — standalone skill-репозиторий по `Remnawave`.
- [nidox-vpn-skills](https://github.com/JonesPitkin/nidox-vpn-skills) — мета-репозиторий VPN skills, где используется этот фундаментальный модуль.

## Совместимость

Репозиторий приведен к тому же publish-ready шаблону, что и другие standalone skill-репозитории семейства NIDOX Skills:

- корневой `SKILL.md` выступает как главный entrypoint;
- присутствует `agents/openai.yaml`;
- добавлены `SKILL_INDEX.md`, `VERSION_MATRIX.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, `RELEASE_v1.0.0.md`;
- существующая база знаний, разделы и reference-файлы сохранены без удаления;
- добавлены новые базовые разделы для VPN, OpenWrt, Cloudflare, sing-box, Podkop, 3x-ui, Remnawave и Nginx Proxy Manager.

## Аудит и качество

- история улучшений: [AUDIT.md](./AUDIT.md)
- итоговая оценка качества: [QUALITY_REPORT.md](./QUALITY_REPORT.md)

## License

Проект лицензирован по лицензии MIT. Полный текст: [LICENSE](./LICENSE)
