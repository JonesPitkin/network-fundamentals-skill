---
name: network-fundamentals
description: "Фундаментальная база знаний по компьютерным сетям на русском языке: OSI, TCP/IP, TCP и UDP, MTU и MSS, NAT и CGNAT, маршрутизация, шлюз по умолчанию, DNS, IPv4, IPv6 и сетевые порты. Использовать для объяснения сетевых концепций, диагностики связности, разбора маршрутов, проблем DNS, NAT, MTU, публикации сервисов и выбора транспортных протоколов."
---

# network-fundamentals

Этот `SKILL.md` является главным entrypoint репозитория. Использовать его как общий вход в сетевую тематику, когда запрос касается базовой сетевой теории, прикладной диагностики или проектирования связности.

## Как работать с этим skill

1. Определить класс проблемы: теория, диагностика, проектирование, публикация сервиса, деградация производительности.
2. Если проблема не локализована, начать с [osi-model/SKILL.md](./osi-model/SKILL.md).
3. Если нужна реальная стековая модель Интернета, перейти к [tcp-ip/SKILL.md](./tcp-ip/SKILL.md).
4. Для адресации и связности использовать разделы IPv4, IPv6, routing и gateway.
5. Для проблем приложений проверять DNS, TCP/UDP, порты, NAT/CGNAT и MTU.
6. Для безопасной публикации сервисов, VPN-панелей и edge-инфраструктуры использовать TLS, HTTPS, CDN, reverse proxy, firewall и linux-networking.

## Роль entrypoint

- классифицировать запрос и направить его в нужный тематический раздел;
- не дублировать полный материал всех разделов в одном файле;
- удерживать единый диагностический порядок для всего репозитория;
- использовать [README.md](./README.md) и [SKILL_INDEX.md](./SKILL_INDEX.md) как карту репозитория.

## Быстрая навигация

- [README.md](./README.md) - обзор навыка, карта тем и порядок изучения
- [SKILL_INDEX.md](./SKILL_INDEX.md) - список всех skills в репозитории
- [VERSION_MATRIX.md](./VERSION_MATRIX.md) - матрица стандартов и release compatibility
- [osi-model/SKILL.md](./osi-model/SKILL.md) - разложение проблем по слоям
- [tcp-ip/SKILL.md](./tcp-ip/SKILL.md) - практический стек Интернета
- [tcp-vs-udp/SKILL.md](./tcp-vs-udp/SKILL.md) - выбор транспорта
- [mtu/SKILL.md](./mtu/SKILL.md) - MTU, MSS, PMTUD
- [nat/SKILL.md](./nat/SKILL.md) - трансляция адресов и портов
- [cgnat/SKILL.md](./cgnat/SKILL.md) - операторский NAT
- [routing/SKILL.md](./routing/SKILL.md) - выбор пути и маршруты
- [gateway/SKILL.md](./gateway/SKILL.md) - шлюз по умолчанию
- [dns/SKILL.md](./dns/SKILL.md) - разрешение имен
- [ipv4/SKILL.md](./ipv4/SKILL.md) - адресация IPv4
- [ipv6/SKILL.md](./ipv6/SKILL.md) - адресация IPv6
- [ports/SKILL.md](./ports/SKILL.md) - транспортные порты
- [tls/SKILL.md](./tls/SKILL.md) - TLS, сертификаты и handshake
- [https/SKILL.md](./https/SKILL.md) - HTTPS, redirects и secure publication
- [cdn/SKILL.md](./cdn/SKILL.md) - CDN, caching и edge delivery
- [reverse-proxy/SKILL.md](./reverse-proxy/SKILL.md) - reverse proxy и upstream routing
- [firewall/SKILL.md](./firewall/SKILL.md) - traffic filtering и policy enforcement
- [linux-networking/SKILL.md](./linux-networking/SKILL.md) - Linux interfaces, routes, sockets и link state
- [references/sources.md](./references/sources.md) - канонические источники

## Разделы репозитория

- `osi-model` - диагностическая модель по слоям
- `tcp-ip` - реальная интернет-стековая модель
- `tcp-vs-udp` - транспорт и выбор протокола
- `dns` - разрешение имен и resolver behavior
- `ports` - сокеты и transport endpoints
- `nat` - address translation
- `cgnat` - operator-side NAT
- `mtu` - packet size, MSS и PMTUD
- `gateway` - default route next hop
- `routing` - route lookup и path selection
- `ipv4` - IPv4 address space
- `ipv6` - IPv6 address space и ICMPv6
- `tls` - encrypted transport и certificate-backed authentication
- `https` - secure web publication поверх TLS
- `cdn` - edge delivery, caching и origin shielding
- `reverse-proxy` - request forwarding и upstream abstraction
- `firewall` - packet filtering и exposure policy
- `linux-networking` - host-side network stack и runtime diagnostics

## Рабочий диагностический порядок

```text
link
  -> L2 adjacency
    -> IP address/prefix
      -> route/default gateway
        -> DNS
          -> TCP/UDP and port
            -> NAT/CGNAT
              -> MTU/MSS/PMTUD
                -> application behavior
```

## Правила качества

- Предпочитать объяснение от простого к техническому, не теряя смысла.
- При нормативных формулировках опираться на RFC.
- При практических примерах явно указывать протокол, адресное семейство, порт и направление трафика.
- Не считать рабочий `ping` доказательством исправности DNS, TCP, TLS или приложения.
- Для глубокой темы переходить в профильный раздел, а не расширять entrypoint до encyclopedic duplicate.

## Ссылки

- [README.md](./README.md)
- [SKILL_INDEX.md](./SKILL_INDEX.md)
- [references/repository-map.md](./references/repository-map.md)
- [references/standalone-compatibility.md](./references/standalone-compatibility.md)
