# Slotr Visual Redesign — Design Spec

> **Date:** 2026-05-20
> **Status:** Approved
> **Branch:** main

## Overview

Rediseño visual completo de `src/pages/slotr.astro` manteniendo la estructura de contenido existente (17 features en 5 categorías). Estilo bento grid con cards de categoría de tamaño variable, hero animado con CSS, e iconos SVG reemplazando emojis.

## Hero Section

### Layout
- Fondo: `#0a0a0f` (near-black)
- 4 formas circulares animadas con `radial-gradient` en tonos violeta
- Grid overlay sutil (60px) con máscara radial
- 3 iconos SVG flotando con opacidad baja (0.10-0.15)

### Contenido
- Badge pill: `SaaS · Agendamiento` — borde violeta, uppercase, tracking-wider
- Título: "Turnos online, sin complicaciones" — gradiente white → #c084fc → #7c3aed
- Subtítulo: texto muted, max-width 28rem
- CTA: "Consultá por una demo" — gradiente #7c3aed → #a855f7, sombra violeta

### Animaciones
- CSS-only `@keyframes float` (20s ease-in-out infinite)
- Formas se mueven en translate + scale con diferentes duraciones
- Iconos flotantes heredan la misma animación

## Bento Grid — Feature Categories

### Concepto
Cada categoría es una **card contenedora** con sus features como **sub-cards** internas. El tamaño de la card varía según la cantidad de features.

### Grid System
- Grid de 12 columnas
- Gap: 1rem
- Las cards se posicionan con `grid-column: span N`

### Card Sizes
| Categoría | Features | Span | Sub-grid |
|---|---|---|---|
| Gestión | 5 | span 7 | 3 columnas |
| Comunicación | 4 | span 5 | 2 columnas |
| Reservas | 4 | span 5 | 2 columnas |
| Marketing | 2 | span 4 | 2 columnas |
| Analytics | 2 | span 3 | 1 columna |

### Card Styles
- **Normal:** `bg-white/[0.03] border border-white/[0.06] rounded-2xl`
- **Marketing (Nuevo):** `bg-gradient-to-br from-violet-500/10 to-purple-500/5 border-violet-500/25`
- **Hover:** `hover:border-violet-500/30 hover:-translate-y-0.5 transition-all`

### Sub-card Styles
- Fondo: `bg-white/[0.02] border border-white/[0.04] rounded-xl`
- Padding: 0.75rem
- Icono SVG 16px stroke violet
- Título: 0.7rem font-bold
- Descripción: 0.6rem color #777, line-height 1.4

### Category Header
- Icono SVG 20px stroke #a855f7
- Título categoría: 1rem font-bold
- Descripción categoría: 0.7rem color #666
- Badge "Nuevo" (solo Marketing): bg-violet-500/20, text-violet-300, uppercase

## Icon System

Todos los emojis se reemplazan por SVG inline estilo Lucide (stroke 1.5px, rounded corners).

| Feature | SVG Icon |
|---|---|
| Reservas online | `calendar` |
| Múltiples servicios | `list` |
| Multi-servicios | `link` |
| Categorías y precios | `folder` |
| Gestión de agenda | `calendar-days` |
| Staff y recursos | `users` |
| Panel administrativo | `settings` |
| Bloqueos con motivo | `lock` |
| Permisos granulares | `shield` |
| Notificaciones | `bell` |
| Confirmación por email | `mail` |
| Recordatorios automáticos | `clock` |
| Confirmación por WhatsApp | `message-circle` |
| Eventos y Promociones | `sparkles` |
| Reseñas de clientes | `star` |
| Dashboard de métricas | `activity` |
| Personalización | `palette` |

## Pricing Section

- Cards con estilo consistente al bento grid
- Featured row (2-3 recursos): fondo violeta sutil, borde violeta
- Links "Consultá →" con color violet en featured

## CTA Section

- Texto centrado, borde superior
- Título grande, subtítulo muted
- Botones de contacto (ContactButtons component)

## Constraints

- 100% estático (Astro), sin JS runtime
- Cloudflare Pages compatible
- Sin emojis como iconos
- Sin look genérico de IA

## Files to Modify

| File | Change |
|---|---|
| `src/pages/slotr.astro` | Hero, bento grid, pricing, CTA |
| `src/components/FeatureCard.astro` | Reemplazar emoji por SVG o deprecar |
| `src/styles/global.css` | Animaciones, nuevos estilos |
