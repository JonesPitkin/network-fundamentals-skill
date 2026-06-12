# Version Matrix

| Area | Baseline | Source of Truth |
|---|---|---|
| Codex repository format | standalone publish-ready | this repository |
| Root entrypoint | `SKILL.md` | this repository |
| Topic sections | 24 preserved and extended sections | this repository |
| Normative protocol definitions | current RFCs | `references/sources.md` |
| Practical Linux/OpenWrt guidance | current docs at source time | `references/sources.md` |
| Web security and edge publication guidance | current official docs at source time | MDN, Cloudflare, NGINX, OpenWrt firewall docs |
| Internet routing and secure DNS guidance | current official docs at source time | Cloudflare, Cisco, RFC Editor |
| Local repository release | `v1.0.0` | this repository |

## Policy

- Репозиторий фиксирует publish-ready структуру, но не замораживает весь Интернет в одну статичную спецификацию.
- При расхождении между локальным объяснением и RFC источником приоритет у RFC.
- При практических сценариях Linux/OpenWrt нужно перепроверять текущий runtime context, даже если теория в репозитории неизменна.
