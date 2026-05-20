# Slotr Page Update Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the Slotr landing page to display all 17 features organized into 5 thematic categories with a "Nuevo" badge on Eventos.

**Architecture:** Replace the single flat features array with a `featureCategories` array. Each category renders its own section with heading, description, and FeatureCard grid. Only the features section of `slotr.astro` changes; all other sections, components, and layout remain untouched.

**Tech Stack:** Astro, Tailwind CSS 4

---

### Task 1: Replace flat features with categorized data structure

**Files:**
- Modify: `src/pages/slotr.astro:11-21`

- [ ] **Step 1: Replace the `features` array with `featureCategories`**

Replace lines 11-21 (the `features` array) with this categorized data:

```javascript
const featureCategories = [
  {
    heading: 'Reservas',
    description: 'Todo para que tus clientes reserven fácil.',
    features: [
      { icon: '📅', name: 'Reservas online', description: 'Página pública donde tus clientes reservan su turno sin llamar.' },
      { icon: '🛎️', name: 'Múltiples servicios', description: 'Servicios con duración y rango de precios. Con 10 o más servicios, los clientes navegan por categoría primero.' },
      { icon: '🧩', name: 'Multi-servicios', description: 'Tus clientes pueden reservar varios servicios en una sola cita. El sistema calcula duración total y precio combinado automáticamente.' },
      { icon: '📂', name: 'Categorías y precios', description: 'Organizá tus servicios por categoría y mostrá rangos de precio para que el cliente tenga una idea clara antes de reservar.' },
    ],
  },
  {
    heading: 'Gestión',
    description: 'Control total de tu equipo y tu agenda.',
    features: [
      { icon: '📆', name: 'Gestión de agenda', description: 'Vista de calendario por recurso con bloqueos y cancelaciones.' },
      { icon: '👥', name: 'Staff y recursos', description: 'Soporte para personas y recursos físicos, con roles admin/staff y permisos granulares por módulo.' },
      { icon: '⚙️', name: 'Panel administrativo', description: 'Configuración completa: horarios, servicios, bloqueos y ajustes del negocio.' },
      { icon: '🚫', name: 'Bloqueos con motivo', description: 'Bloqueá turnos individuales o días completos indicando el motivo. Visible en la agenda para todo el equipo.' },
      { icon: '🔐', name: 'Permisos granulares', description: 'Controlá quién ve y gestiona cada agenda. Permisos independientes por staff para agenda, bloqueos y configuración.' },
    ],
  },
  {
    heading: 'Comunicación',
    description: 'Mantené informados a tus clientes y a tu equipo.',
    features: [
      { icon: '🔔', name: 'Notificaciones', description: 'Avisos instantáneos por Telegram al staff cuando un cliente reserva. Integración con bot de Telegram para mantener al equipo informado en tiempo real.' },
      { icon: '📧', name: 'Confirmación por email', description: 'Tus clientes reciben un email con los detalles de su turno al confirmar la reserva.' },
      { icon: '⏰', name: 'Recordatorios automáticos', description: 'Emails de recordatorio enviados automáticamente antes del turno para reducir ausencias.' },
      { icon: '💬', name: 'Confirmación por WhatsApp', description: 'Botón directo en la pantalla de confirmación para que el cliente envíe los datos de su turno por WhatsApp.' },
    ],
  },
  {
    heading: 'Marketing',
    description: 'Atraé más clientes y fidelizá a los que ya tenés.',
    features: [
      { icon: '🎉', name: 'Eventos y Promociones', description: 'Creá promociones con descuentos porcentuales o fijos, notificaciones visuales con íconos y banners de color. Solo un evento activo a la vez. Tus clientes ven las ofertas directamente en la página de reservas.', isNew: true },
      { icon: '⭐', name: 'Reseñas de clientes', description: 'Los clientes califican su experiencia con estrellas y texto. El puntaje promedio y las reseñas recientes se muestran en tu página pública.' },
    ],
  },
  {
    heading: 'Analytics',
    description: 'Datos claros para tomar mejores decisiones.',
    features: [
      { icon: '📊', name: 'Dashboard de métricas', description: 'KPIs de turnos e ingresos estimados, 5 gráficos por período (7/30/90 días), ranking de servicios, franjas horarias pico y clientes frecuentes.' },
      { icon: '🎨', name: 'Personalización', description: '16 paletas de color, logo propio y etiquetas configurables. Tu sistema de turnos con tu identidad visual.' },
    ],
  },
];
```

Note: The Eventos feature has `isNew: true` which will drive the badge rendering.

- [ ] **Step 2: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "refactor(slotr): replace flat features with categorized data structure"
```

---

### Task 2: Update the features section template to render categories

**Files:**
- Modify: `src/pages/slotr.astro:58-65`

- [ ] **Step 1: Replace the single features grid with category sections**

Replace lines 58-65 (the FUNCIONALIDADES section) with this:

```html
    <!-- FUNCIONALIDADES -->
    <section class="py-16">
      <h2 class="text-xl font-black mb-2">¿Qué incluye Slotr?</h2>
      <p class="text-sm text-muted mb-8">Todo lo que necesitás para que tus clientes reserven solos.</p>
    </section>

    {featureCategories.map(cat => (
      <section class="py-12 border-t border-border">
        <h2 class="text-xl font-black mb-1">
          {cat.heading}
          {cat.heading === 'Marketing' && (
            <span class="inline-block px-2 py-0.5 rounded text-[10px] font-bold uppercase tracking-wider bg-slotr/20 text-slotr align-middle ml-2">Nuevo</span>
          )}
        </h2>
        <p class="text-sm text-muted mb-6">{cat.description}</p>
        <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {cat.features.map(f => <FeatureCard {...f} />)}
        </div>
      </section>
    ))}
```

Key decisions:
- The "Nuevo" badge is on the "Marketing" category heading (not on individual cards) for cleaner visual hierarchy.
- Each category section has `border-t border-border` to separate visually.
- The first section (title + subtitle) keeps `py-16` and no border. Subsequent categories use `py-12` with top borders.
- `FeatureCard` receives all props via spread, including `isNew` which is ignored by the component (no change needed to FeatureCard).

- [ ] **Step 2: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "feat(slotr): render features as categorized sections with Nuevo badge"
```

---

### Task 3: Verify build

**Files:**
- No file changes

- [ ] **Step 1: Run the build**

```bash
npm run build
```

Expected: Build completes without errors, output in `dist/`.

- [ ] **Step 2: Verify dist output**

```bash
Test-Path "dist/slotr/index.html"
```

Expected: `True` — the slotr page exists in the build output.

- [ ] **Step 3: Commit (if any cleanup needed)**

Only if changes were made during verification:

```bash
git add .
git commit -m "fix: slotr page build verification"
```
