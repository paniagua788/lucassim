# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # servidor de desarrollo en http://localhost:4321
npm run build    # build de producción → dist/
npm run preview  # previsualizar el build de producción localmente
```

No hay test suite ni linter configurado. El equivalente de "test" es `npm run build` — si compila sin errores, el código es correcto.

## Architecture

Sitio estático de 3 páginas construido con **Astro 6** + **Tailwind CSS 4**. Sin backend, sin JavaScript en el cliente.

**Páginas** (`src/pages/`): cada archivo `.astro` es una ruta. `index.astro` = home, `vareapp.astro` = `/vareapp`, `slotr.astro` = `/slotr`.

**Layout** (`src/layouts/BaseLayout.astro`): envuelve todas las páginas. Importa `src/styles/global.css`, carga la fuente Inter desde Google Fonts, y define `<html>/<body>` con `bg-base text-white`.

**Componentes reutilizables** (`src/components/`):
- `Navbar.astro` — prop `showBack: boolean`. `false` = links de navegación (home); `true` = solo "← Volver" con `href="/"` (páginas de producto).
- `Footer.astro` — prop `showHomeLink: boolean`. Socials con `href="#"` + `aria-disabled="true"` mientras no estén configurados.
- `ContactButtons.astro` — props `whatsapp` (URL completa `https://wa.me/...`) y `email` (dirección sin `mailto:`, el componente lo agrega).
- `FeatureCard.astro` — props `icon`, `name`, `description`.
- `ProductCard.astro` — prop `accent: 'vareapp' | 'slotr'` controla colores.

## Design tokens (Tailwind 4)

Los tokens están en `src/styles/global.css` bajo `@theme`. Clases disponibles:

| Token | Clase | Valor |
|---|---|---|
| `--color-base` | `bg-base` | `#111111` |
| `--color-surface` | `bg-surface` | `#161616` |
| `--color-border` | `border-border` | `#2a2a2a` |
| `--color-muted` | `text-muted` | `#888888` |
| `--color-subtle` | `text-subtle` | `#555555` |
| `--color-vareapp` | `bg-vareapp` / `text-vareapp` | `#f97316` |
| `--color-slotr` | `bg-slotr` / `text-slotr` | `#7c3aed` |
| `--radius-card` | `rounded-card` | `12px` |
| `--radius-inner` | `rounded-inner` | `8px` |

> Tailwind 4 usa `@theme` en CSS en lugar de `tailwind.config.js`. No crear `tailwind.config.mjs`.

## Deploy

Cloudflare Pages — deploy automático en cada push a `main`. Dominio: `lucassim.com.py`.

## Contenido a actualizar

Los datos de contacto y links sociales están hardcodeados en cada página. Para actualizar:
- WhatsApp / email: constantes `WHATSAPP` y `EMAIL` al tope de cada `.astro` en `src/pages/`
- Socials: array `socials` en `src/components/Footer.astro`
