# Standalone Compatibility

Репозиторий приведен к тому же publish-ready standalone-паттерну, что и другие skill-репозитории семейства NIDOX Skills:

- корневой `SKILL.md` как entrypoint;
- `agents/openai.yaml` на уровне репозитория;
- индексные и release metadata-файлы в корне;
- локальный каталог `references/`;
- отдельные тематические модули, каждый со своим `SKILL.md`.

При этом для `network-fundamentals-skill` сохранена существующая академическая структура:

- `references.md`
- `glossary.md`
- `examples.md`

Новый publish-ready слой добавлен поверх этих файлов, а не вместо них.
