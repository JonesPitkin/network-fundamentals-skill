---
name: bgp
description: "Объяснять BGP: автономные системы, path selection, Internet routing и влияние BGP на CDN, anycast, reachability и глобальную доступность сервисов."
---

# BGP

## 1. Что это такое

`BGP` — Border Gateway Protocol, основной междоменный протокол маршрутизации Интернета. RFC 4271 определяет BGP-4 как протокол обмена маршрутной информацией между автономными системами.

## 2. Зачем это нужно

- связывать автономные системы в Интернет;
- выбирать путь до удалённых сетей;
- поддерживать глобальную reachability для CDN, DNS, облаков и провайдеров;
- обеспечивать публикацию anycast и multi-network edge infrastructure.

## 3. Как это связано с VPN-инфраструктурой

- BGP косвенно определяет, как пользователи доходят до DNS, CDN, panels и public endpoints вокруг VPN;
- глобальная доступность `3x-ui`, `Remnawave`, subscription pages и Cloudflare-backed publication зависит от междоменной маршрутизации;
- ошибки на Internet routing layer могут выглядеть как “панель недоступна из одной страны/сети”.

## 4. Как это связано с OpenWrt

- OpenWrt обычно не является Internet-scale BGP router, но его пользователи зависят от результатов BGP path selection upstream;
- на OpenWrt важно уметь объяснять, почему разные провайдеры или uplinks видят разные paths до одного сервиса;
- это полезно при анализе multi-WAN, CDN reachability и region-specific incidents.

## 5. Как это связано с Cloudflare

- Cloudflare использует BGP вместе с anycast для маршрутизации трафика к edge;
- поведение anycast напрямую зависит от Internet routing и peering relationships;
- Cloudflare explicitly warns, что трафик не всегда идёт в интуитивно “ближайший” дата-центр.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `sing-box` и `Podkop` часто используются в сценариях, где route quality, latency и reachability важны;
- `3x-ui` и `Remnawave` зависят от стабильной интернет-маршрутизации для web/control-plane exposure;
- понимание BGP помогает объяснять региональные деградации, разные latency paths и edge anomalies.

## 7. Типовые ошибки

- думать, что Интернет всегда выбирает географически самый короткий путь;
- путать BGP с внутренней статической или OSPF-маршрутизацией;
- считать latency единственным фактором path selection;
- игнорировать peering/policy differences между операторами.

## 8. Диагностика

1. Проверить, локальна ли проблема или зависит от сети/региона.
2. Отличить origin/service failure от Internet path anomaly.
3. Помнить, что traceroute показывает observed path, но не всю policy logic.
4. Учитывать anycast/CDN behavior.
5. При Internet-wide вопросах смотреть на BGP и external routing context, а не только на host firewall.

## 9. Практические примеры

- Почему один ISP видит Cloudflare edge быстро, а другой — медленнее.
- Почему anycast DNS может приводить к разным POP для разных провайдеров.
- Почему панель доступна из одного региона и проблемна из другого при одинаковом origin.
- Объяснение, почему “ближайший по карте” data center не обязан быть выбран.

## 10. Checklist для Codex

- Уточнить, проблема локальная или Internet-path-specific.
- Не смешивать BGP с host routing table.
- Учитывать anycast, CDN и peering.
- При необходимости перейти в [../anycast/SKILL.md](../anycast/SKILL.md), [../cdn/SKILL.md](../cdn/SKILL.md) и [../routing/SKILL.md](../routing/SKILL.md).
