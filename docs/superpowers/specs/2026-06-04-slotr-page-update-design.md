# Slotr Page Update — Design Spec

**Date:** 2026-06-04
**Status:** Draft — pending user review
**File:** `src/pages/slotr.astro`

## Objective

Update the Slotr landing page to reflect all 17 current features of the SaaS, organized into 5 thematic categories. The Events/Promotions module (Phase 8) is the primary new addition.

## Architecture

### Sections (top to bottom)

1. **Hero** — unchanged. Logo, tagline, CTA "Consultá por una demo".
2. **¿Qué incluye Slotr?** — 5 category blocks, each with a heading and a grid of FeatureCards.
3. **Para quién es** — unchanged.
4. **Precio según tu equipo** — unchanged.
5. **CTA Final** — unchanged.

### Feature Categorization

#### 📅 Reservas (4 features)
| Icon | Name | Description |
|---|---|---|
| 📅 | Reservas online | Página pública donde tus clientes reservan su turno sin llamar. |
| 🛎️ | Múltiples servicios | Servicios con duración y rango de precios. Con 10 o más servicios, los clientes navegan por categoría primero. |
| 🧩 | Multi-servicios | Tus clientes pueden reservar varios servicios en una sola cita. El sistema calcula duración total y precio combinado automáticamente. |
| 📂 | Categorías y precios | Organizá tus servicios por categoría y mostrá rangos de precio para que el cliente tenga una idea clara antes de reservar. |

#### ⚙️ Gestión (5 features)
| Icon | Name | Description |
|---|---|---|
| 📆 | Gestión de agenda | Vista de calendario por recurso con bloqueos y cancelaciones. |
| 👥 | Staff y recursos | Soporte para personas y recursos físicos, con roles admin/staff y permisos granulares por módulo. |
| ⚙️ | Panel administrativo | Configuración completa: horarios, servicios, bloqueos y ajustes del negocio. |
| 🚫 | Bloqueos con motivo | Bloqueá turnos individuales o días completos indicando el motivo. Visual en la agenda para todo el equipo. |
| 🔐 | Permisos granulares | Controlá quién ve y gestiona cada agenda. Permisos independientes por staff para agenda, bloqueos y configuración. |

#### 📢 Comunicación (4 features)
| Icon | Name | Description |
|---|---|---|
| 🔔 | Notificaciones | Avisos instantáneos por Telegram al staff cuando un cliente reserva. Integración con bot de Telegram para mantener al equipo informado en tiempo real. |
| 📧 | Confirmación por email | Tus clientes reciben un email con los detalles de su turno al confirmar la reserva. |
| ⏰ | Recordatorios automáticos | Emails de recordatorio enviados automáticamente antes del turno para reducir ausencias. |
| 💬 | Confirmación por WhatsApp | Botón directo en la pantalla de confirmación para que el cliente envíe los datos de su turno por WhatsApp. |

#### 🎉 Marketing (2 features)
| Icon | Name | Description |
|---|---|---|
| 🎉 | Eventos y Promociones | **NUEVO** — Creá promociones con descuentos porcentuales o fijos, notificaciones visuales con íconos y banners de color. Solo un evento activo a la vez. Tus clientes ven las ofertas directamente en la página de reservas. |
| ⭐ | Reseñas de clientes | Los clientes califican su experiencia con estrellas y texto. El puntaje promedio y las reseñas recientes se muestran en tu página pública. |

#### 📊 Analytics (2 features)
| Icon | Name | Description |
|---|---|---|
| 📊 | Dashboard de métricas | KPIs de turnos e ingresos estimados, 5 gráficos por período (7/30/90 días), ranking de servicios, franjas horarias pico y clientes frecuentes. |
| 🎨 | Personalización | 16 paletas de color, logo propio y etiquetas configurables. Tu sistema de turnos con tu identidad visual. |

### Data Structure

```javascript
const featureCategories = [
  {
    heading: 'Reservas',
    description: 'Todo para que tus clientes reserven fácil.',
    features: [
      { icon: '📅', name: 'Reservas online', description: '...' },
      { icon: '🛎️', name: 'Múltiples servicios', description: '...' },
      { icon: '🧩', name: 'Multi-servicios', description: '...' },
      { icon: '📂', name: 'Categorías y precios', description: '...' },
    ],
  },
  // ... 4 more categories
];
```

### Rendering

Each category renders as:

```html
<section class="py-12 border-t border-border">
  <h2 class="text-xl font-black mb-1">
    {heading}
    <span class="text-xs font-bold text-slotr ml-2" if="is Marketing">NUEVO</span>
  </h2>
  <p class="text-sm text-muted mb-6">{description}</p>
  <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
    {features.map(f => <FeatureCard {...f} />)}
  </div>
</section>
```

The "NUEVO" badge appears only on the Marketing category heading (or on the Eventos card itself).

### Badge Implementation

The "NUEVO" badge renders as:
```html
<span class="inline-block px-2 py-0.5 rounded text-[10px] font-bold uppercase tracking-wider bg-slotr/20 text-slotr">Nuevo</span>
```

Applied to the Eventos feature card or the Marketing section heading.

## What Stays Unchanged

- Hero section (logo, tagline, CTA)
- "Para quién es" section
- Pricing section
- CTA final section
- Navbar, Footer, ContactButtons components
- FeatureCard component (reused as-is)
- Color tokens and Tailwind classes

## What Changes

- Single features grid → 5 categorized sections with headings and descriptions
- 9 features → 17 features total
- 8 new features added: Eventos/Promociones, Multi-servicios, Categorías y precios, Email confirmación, Email reminders, WhatsApp confirmación, Bloqueos con motivo, Permisos granulares
- "Nuevo" badge on Eventos feature

## Verification

1. `npm run build` completes without errors.
2. `npm run dev` — all 5 category sections render correctly.
3. Responsive: grid collapses to 1 column on mobile, 2 on tablet, 3 on desktop.
4. "Nuevo" badge visible on Eventos.
