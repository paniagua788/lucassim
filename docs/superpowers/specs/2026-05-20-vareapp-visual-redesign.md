# VareApp Visual Redesign — Design Spec

> **Date:** 2026-05-20
> **Status:** Approved
> **Branch:** main

## Overview

Rediseño visual completo de `src/pages/vareapp.astro` siguiendo el mismo patrón que Slotr: hero animado con CSS, bento grid de categorías con tamaño variable, iconos SVG Lucide reemplazando emojis. Color brand: naranja (`#f97316`).

## Hero Section

### Layout
- Fondo: `#0a0a0f` (near-black)
- 4 formas circulares animadas con `radial-gradient` en tonos naranja
- Grid overlay sutil (60px) con máscara radial
- 5 iconos SVG flotando con opacidad baja (0.10-0.15)

### Iconos Flotantes (food-themed)
| Icon | Color | Posición |
|---|---|---|
| `chef-hat` | `#fb923c` | top-right |
| `utensils-crossed` | `#f97316` | bottom-left |
| `flame` | `#ea580c` | top-left |
| `coffee` | `#fb923c` | bottom-right |
| `pizza` | `#f97316` | mid-left |

### Contenido
- Badge pill: `SaaS · Gastronomía` — borde naranja, uppercase, tracking-wider
- Logo VareApp (imagen existente)
- Título: "Menú digital y pedidos para tu negocio" — gradiente white → #fb923c → #f97316
- Subtítulo: texto muted, max-width 28rem
- CTA: "Consultá por una demo" — gradiente #f97316 → #ea580c, sombra naranja

### Animaciones
- CSS-only `@keyframes float` (mismo que Slotr)
- `prefers-reduced-motion` support

## Bento Grid — Feature Categories

### Concepto
Cada categoría es una card contenedora con sus features como sub-cards internas. Tamaño variable según cantidad de features.

### Grid System
- Grid de 12 columnas
- Gap: 1rem
- Responsive: `grid-cols-1 lg:grid-cols-12`

### Categories
| Categoría | Features | Span | Icon |
|---|---|---|---|
| Pedidos (4) | Menú digital, Gestión de pedidos, Modo mozo, Tickets de cocina | 5 | `book-open` |
| Operaciones (4) | Panel administrativo, Caja, Inventario, Impresión automática | 7 | `settings` |
| Negocio (2) | Métricas, Personalización | 6 | `bar-chart-3` |
| Marketing (1) | Generador de flyers | 6 | `image` |

### Layout Rows
- Row 1: Pedidos (5) + Operaciones (7) = 12
- Row 2: Negocio (6) + Marketing (6) = 12

### Card Styles
- **Normal:** `bg-white/[0.03] border border-white/[0.06] rounded-2xl`
- **Marketing (destacada):** `bg-gradient-to-br from-orange-500/10 to-amber-500/5 border-orange-500/25`
- **Hover:** `hover:border-orange-500/30 hover:-translate-y-0.5 transition-all`

### Sub-card Styles
- Fondo: `bg-white/[0.02] border border-white/[0.04] rounded-xl`
- Padding: 0.75rem
- Icono SVG 16px stroke naranja
- Título: 0.7rem font-bold
- Descripción: 0.6rem color #777, line-height 1.4

## Icon System

11 features → SVG inline Lucide-style (stroke 1.5px, rounded corners).

| Feature | Icon Name |
|---|---|
| Menú digital | `book-open` |
| Gestión de pedidos | `clipboard-list` |
| Panel administrativo | `settings` |
| Caja | `credit-card` |
| Inventario | `package` |
| Métricas | `bar-chart-3` |
| Modo mozo | `user-check` |
| Tickets de cocina | `printer` |
| Impresión automática | `bot` |
| Personalización | `palette` |
| Generador de flyers | `image` |

5 floating hero icons: `chef-hat`, `utensils-crossed`, `flame`, `coffee`, `pizza`

## Pricing Section

- Cards con estilo consistente al bento grid
- Plan Pro (featured): fondo naranja sutil, borde naranja
- Links "Consultar" con color naranja en featured

## CTA Section

- Texto centrado, borde superior
- Título grande, subtítulo muted
- Botones de contacto (ContactButtons component)

## Constraints

- 100% estático (Astro), sin JS runtime
- Cloudflare Pages compatible
- Sin emojis como iconos
- Reutilizar CategoryCard existente (adaptar colores naranja)
- Reutilizar animaciones CSS existentes (agregar variantes naranja)

## Files to Modify

| File | Change |
|---|---|
| `src/styles/global.css` | Add VareApp orange animation/card/CTA classes |
| `src/components/vareapp-icons.ts` | Create: 11 feature SVG icons + 5 hero food icons |
| `src/pages/vareapp.astro` | Hero, bento grid, pricing, CTA |
