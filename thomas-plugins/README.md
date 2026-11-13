# Plugins perso (Thomas)

Ajouts propres à ce fork, déclarés dans `.claude-plugin/marketplace.json` à côté du plugin `ecc`.

| Plugin | Contenu | Source |
|--------|---------|--------|
| `gsap-skills` | 8 skills officiels GSAP (aucun hook, aucun MCP) | <https://github.com/greensock/gsap-skills> |
| `site-animations` | Skill qui intègre GSAP + Lenis + React Bits dans un site | ce dossier |

Lenis et React Bits ne sont pas des plugins Claude Code : ils s'installent dans chaque projet de site (npm / shadcn). Le skill `site-animations` s'en charge.

## Installation sur un PC (marketplace `ecc` déjà ajouté)

Dans Claude Code :

```text
/plugin marketplace update ecc
/plugin install gsap-skills@ecc
/plugin install site-animations@ecc
```

Puis redémarrer Claude Code.

## Utilisation

Ouvrir Claude Code dans le dossier du site, puis :

```text
Utilise le skill site-animations pour intégrer GSAP, Lenis et React Bits à mon site.
Demande-moi mon accord avant chaque installation ou modification.
```
