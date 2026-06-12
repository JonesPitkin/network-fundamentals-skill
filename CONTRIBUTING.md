# Contributing

- Не удалять существующую базу знаний, разделы и reference-файлы без явной миграции.
- Сохранять все 12 тематических разделов:
  `osi-model`, `tcp-ip`, `tcp-vs-udp`, `dns`, `ports`, `nat`, `cgnat`, `mtu`, `gateway`, `routing`, `ipv4`, `ipv6`.
- Новые материалы писать на русском языке, сохраняя технические команды, RFC names и network terminology на английском языке.
- Нормативные определения сверять по RFC; прикладные объяснения и operational analogies можно опирать на уже перечисленные источники из `references/sources.md`.
- Корневой `SKILL.md` должен оставаться главным repository entrypoint, а глубина темы должна жить в профильных разделах.
- Не переносить и не удалять существующие `references.md`, `glossary.md`, `examples.md`; новые publish-ready слои должны добавляться поверх них.
