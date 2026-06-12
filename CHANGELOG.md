# Changelog

## v1.0.0

- репозиторий приведен к publish-ready standalone-стандарту;
- сохранены все 12 тематических разделов и существующие reference-файлы;
- корневой `SKILL.md` закреплен как главный entrypoint;
- добавлены `agents/openai.yaml` и compatibility metadata;
- добавлены `SKILL_INDEX.md`, `VERSION_MATRIX.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, `RELEASE_v1.0.0.md`;
- в каждый тематический раздел добавлены каталоги `agents/` и `references/` без удаления прежних `references.md`, `glossary.md`, `examples.md`;
- `README.md` обновлен под publish-ready публикацию на GitHub.

## Unreleased

- добавлены новые фундаментальные разделы:
  - `tls`
  - `https`
  - `cdn`
  - `reverse-proxy`
  - `firewall`
  - `linux-networking`
- для каждого нового раздела добавлены `SKILL.md`, `agents/openai.yaml`, `references/official-links.md`;
- обновлены `README.md`, `SKILL.md`, `SKILL_INDEX.md` и `VERSION_MATRIX.md` под 18-раздельный базовый skill.
- добавлены новые advanced-фундаментальные разделы:
  - `anycast`
  - `bgp`
  - `dns-security`
  - `mtls`
  - `http2-http3`
  - `load-balancing`
- обновлены `README.md`, `SKILL_INDEX.md`, `VERSION_MATRIX.md` и `references/sources.md` под 24-раздельный базовый skill.
