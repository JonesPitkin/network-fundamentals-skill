---
name: dns-security
description: "Объяснять DNS security: DNSSEC, DoH, DoT, privacy, integrity и secure resolver behavior для клиентов, роутеров и edge-инфраструктуры."
---

# DNS Security

## 1. Что это такое

`DNS security` — это практика защиты DNS infrastructure и DNS traffic. Cloudflare описывает это как набор overlapping defenses, включая redundancy, DNSSEC и operational controls. В этом разделе основной акцент на `DNSSEC`, `DoH` и `DoT`.

## 2. Зачем это нужно

- защищать DNS от подмены, poisoning и некоторых форм tampering;
- повышать доверие к ответам DNS через `DNSSEC`;
- защищать приватность запросов через `DoH` и `DoT`;
- обеспечивать стабильную работу critical name resolution.

## 3. Как это связано с VPN-инфраструктурой

- VPN-клиенты и панели зависят от корректного DNS;
- secure DNS особенно важен для subscription domains, panel domains, API names и upstream resolvers;
- без понимания DNSSEC/DoH/DoT легко спутать privacy, integrity и authenticity в одну функцию.

## 4. Как это связано с OpenWrt

- OpenWrt часто управляет DNS для всей домашней/офисной сети;
- secure DNS choices (`DoH`, `DoT`, validating resolver upstream) напрямую влияют на все устройства за роутером;
- ошибки в firewall, MTU и routing могут проявляться как проблемы с secure DNS.

## 5. Как это связано с Cloudflare

- Cloudflare Learning Center подробно объясняет `DNSSEC`, `DoH` и `DoT`;
- Cloudflare DNS и anycast infrastructure часто используются как пример secure/public resolver layer;
- важно различать `DNSSEC` как защиту целостности ответов и `DoH`/`DoT` как защиту приватности канала.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `sing-box` и `Podkop` сильно зависят от DNS path и privacy/anti-tampering design;
- `3x-ui` и `Remnawave` зависят от корректного разрешения доменных имён панелей, API и subscription services;
- secure DNS особенно важен там, где DNS manipulation может ломать обход, доставку конфигов или доступ к panel domain.

## 7. Типовые ошибки

- считать `DNSSEC` аналогом `DoH` или `DoT`;
- думать, что encrypted DNS автоматически валидирует authenticity ответов;
- игнорировать, что `DoT` и `DoH` всё ещё требуют working IP reachability;
- ломать secure DNS firewall-правилами или MTU issues;
- диагностировать “сломанный Интернет”, когда проблема только в resolver security path.

## 8. Диагностика

1. Определить, речь о privacy, integrity или resolver availability.
2. Разделить `DNSSEC`, `DoH`, `DoT` по назначению.
3. Проверить обычный DNS path и secure DNS path отдельно.
4. Проверить firewall, routing и MTU.
5. Проверить, не на уровне resolver policy ли проблема.

## 9. Практические примеры

- Объяснение разницы между `DNSSEC` и `DoH`.
- Выбор между `DoT` и `DoH` для сети за OpenWrt.
- Разбор случая, когда secure DNS работает нестабильно из-за path issues.
- Проверка, почему panel domain резолвится по обычному DNS, но не через configured secure path.

## 10. Checklist для Codex

- Уточнить: нужны confidentiality, integrity, authenticity или все сразу.
- Не путать DNSSEC с DoH/DoT.
- Для OpenWrt отдельно проговорить роль роутера как общесетевого DNS gatekeeper.
- При необходимости перейти в [../dns/SKILL.md](../dns/SKILL.md), [../anycast/SKILL.md](../anycast/SKILL.md) и [../firewall/SKILL.md](../firewall/SKILL.md).
