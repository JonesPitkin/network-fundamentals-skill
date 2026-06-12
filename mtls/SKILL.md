---
name: mtls
description: "Объяснять mutual TLS: двустороннюю аутентификацию, client certificates и сценарии, где и клиент, и сервер доказывают свою подлинность."
---

# Mutual TLS

## 1. Что это такое

`mTLS` — mutual TLS, режим, в котором не только сервер доказывает свою подлинность клиенту, но и клиент предъявляет сертификат серверу. MDN отмечает, что client authentication на вебе встречается реже, но используется в специализированных сценариях.

## 2. Зачем это нужно

- усиливать доступ к чувствительным admin/API endpoints;
- аутентифицировать service-to-service connections;
- ограничивать доступ к management plane без опоры только на пароль или token;
- строить более строгую trust model.

## 3. Как это связано с VPN-инфраструктурой

- mTLS полезен для защищённого control plane, внутренних API и service-to-service traffic;
- это актуально там, где панель, agents или internal tooling обмениваются чувствительными данными;
- mTLS не равен обычному HTTPS: он требует trust к client certificate.

## 4. Как это связано с OpenWrt

- OpenWrt может быть клиентом к mTLS-protected services или точкой, через которую идёт такой трафик;
- важно понимать, что mTLS failures могут проявляться как seemingly generic TLS/HTTP errors;
- при использовании secure upstream services на роутере mTLS добавляет отдельный слой аутентификации.

## 5. Как это связано с Cloudflare

- Cloudflare экосистема часто заставляет отдельно думать о browser-to-edge и service-to-origin trust;
- mTLS особенно полезен для origin/API relationships и sensitive management paths;
- при Cloudflare-publication важно понимать, где mTLS вообще применим: browser, edge или origin-side service mesh.

## 6. Как это связано с sing-box, Podkop, 3x-ui и Remnawave

- `3x-ui` и `Remnawave` могут выиграть от более жёсткой защиты внутренних admin/API paths;
- `sing-box` и `Podkop` могут взаимодействовать с internal tooling или secured APIs, где нужен stronger auth;
- для `Nginx Proxy Manager` mTLS — это отдельный advanced layer, а не обычный HTTPS toggle.

## 7. Типовые ошибки

- путать mTLS с обычным TLS;
- ожидать, что browser user flow всегда дружелюбен к client certificates;
- не разделять public web publication и internal service authentication;
- забывать, что обе стороны должны доверять certificate chain.

## 8. Диагностика

1. Проверить, требуется ли client certificate.
2. Проверить certificate trust на обеих сторонах.
3. Отделить TLS failure от client-auth failure.
4. Проверить, на каком hop применяется mTLS.
5. Не смешивать browser-facing HTTPS и service-facing mTLS.

## 9. Практические примеры

- Защита internal admin/API endpoint за reverse proxy с client certificate.
- Разбор, почему обычный browser login не проходит к mTLS-protected route.
- Объяснение, где mTLS уместен для control plane, а где достаточно обычного HTTPS.
- Сервисное взаимодействие между internal components через client cert auth.

## 10. Checklist для Codex

- Уточнить, нужен ли public HTTPS или именно mutual auth.
- Проверить, кто client и кто server в trust model.
- Не путать mTLS с просто “включён TLS”.
- При необходимости перейти в [../tls/SKILL.md](../tls/SKILL.md), [../https/SKILL.md](../https/SKILL.md) и [../reverse-proxy/SKILL.md](../reverse-proxy/SKILL.md).
