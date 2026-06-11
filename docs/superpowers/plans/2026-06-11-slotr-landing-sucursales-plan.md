# Slotr Landing — Sucursales Category Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a new "Sucursales" category to the slotr landing page with badge "Nuevo" and 4 features highlighting multi-branch capabilities.

**Architecture:** Modify existing static Astro landing page (`src/pages/slotr.astro`) to include a new feature category in the bento grid. Add two new Lucide icons (`building` and `mapPin`) to the icon system. Maintain the existing 100% static Astro architecture with no runtime changes.

**Tech Stack:** Astro 6, Tailwind CSS 4, TypeScript strict, existing component patterns (CategoryCard.astro, icons.ts)

---

### Task 1: Add new icons to icons.ts

**Files:**
- Modify: `src/components/icons.ts:38`

- [ ] **Step 1: Write the failing test**

```typescript
def test_icons_includes_building_and_map_pin():
    import { icons } from 'src/components/icons'
    assert 'building' in icons
    assert 'mapPin' in icons
    assert icons.building.includes('building')
    assert icons.mapPin.includes('mapPin')
```

- [ ] **Step 2: Run test to verify it fails**

Run: `npm run test` or `npx astro check` (if available)
Expected: FAIL with "'building' is missing from object"

- [ ] **Step 3: Write minimal implementation**

```typescript
export const icons = {
  // ... existing 17 icons ...
  building: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>`,
  mapPin: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2C8 6 5 9.5 5 14a7 7 0 0 0 14 0c0-4.5-3-8-7-12z"/><circle cx="12" cy="14" r="4"/></svg>`,
  // ... rest of existing icons ...
} as const;
```

- [ ] **Step 4: Run test to verify it passes**

Run: `npm run test` or `npx astro check`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add src/components/icons.ts
git commit -m "feat: add building and mapPin icons for slotr sucursales"
```

### Task 2: Update slotr.astro ES category array

**Files:**
- Modify: `src/pages/slotr.astro:27-86`

- [ ] **Step 1: Write the failing test**

```typescript
def test_slotr_feature_categories_includes_sucursales():
    import { featureCategories } from 'src/pages/slotr.astro'
    sucursales = featureCategories.find(cat => cat.heading === 'Sucursales')
    assert sucursales !== undefined
    assert sucursales.span === 4
    assert sucursales.isNew === true
    assert sucursales.features.length === 4
    assert sucursales.features[0].name === 'Multi-sucursal'
```

- [ ] **Step 2: Run test to verify it fails**

Run: `npm run test` or `npx astro check`
Expected: FAIL with "Cannot find name 'featureCategories'"

- [ ] **Step 3: Write minimal implementation**

```typescript
const featureCategories: FeatureCategory[] = [
  // ... existing categories ...
  {
    heading: 'Sucursales',
    description: 'Varios locales, un solo panel.',
    icon: 'building',
    span: 4,
    isNew: true,
    features: [
      { icon: 'building', name: 'Multi-sucursal', description: 'Configurá todas tus ubicaciones físicas. Cada sucursal con su nombre, horarios y staff propio.' },
      { icon: 'clock',    name: 'Horarios por sucursal', description: 'Cada sucursal tiene su propio horario de atención, independiente de las demás.' },
      { icon: 'users',    name: 'Staff asignado', description: 'Asigná cada profesional a una sucursal específica. El sistema filtra quién atiende dónde.' },
      { icon: 'mapPin',   name: 'Selector público', description: 'Cuando tenés más de una sucursal activa, tus clientes eligen dónde reservar en el primer paso.' },
    ],
  },
  // ... rest of existing categories ...
];
```

- [ ] **Step 4: Run test to verify it passes**

Run: `npm run test` or `npx astro check`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "feat: add sucursales category to slotr landing"
```

### Task 3: Update slotr.astro EN category array

**Files:**
- Modify: `src/pages/slotr.astro:96-155`

- [ ] **Step 1: Write the failing test**

```typescript
def test_slotr_feature_categories_en_includes_branches():
    import { featureCategoriesEn } from 'src/pages/slotr.astro'
    branches = featureCategoriesEn.find(cat => cat.heading === 'Branches')
    assert branches !== undefined
    assert branches.span === 4
    assert branches.isNew === true
    assert branches.features.length === 4
    assert branches.features[0].name === 'Multi-branch'
```

- [ ] **Step 2: Run test to verify it fails**

Run: `npm run test` or `npx astro check`
Expected: FAIL with "Cannot find name 'featureCategoriesEn'"

- [ ] **Step 3: Write minimal implementation**

```typescript
const featureCategoriesEn: FeatureCategory[] = [
  // ... existing EN categories ...
  {
    heading: 'Branches',
    description: 'Multiple locations, one panel.',
    icon: 'building',
    span: 4,
    isNew: true,
    features: [
      { icon: 'building', name: 'Multi-branch', description: 'Configure all your physical locations. Each branch with its own name, hours and staff.' },
      { icon: 'clock',    name: 'Per-branch hours', description: 'Each branch has its own opening hours, independent from the others.' },
      { icon: 'users',    name: 'Assigned staff', description: 'Assign each staff member to a specific branch. The system filters who serves where.' },
      { icon: 'mapPin',   name: 'Public selector', description: 'When you have more than one active branch, your clients pick where to book in the first step.' },
    ],
  },
  // ... rest of existing EN categories ...
];
```

- [ ] **Step 4: Run test to verify it passes**

Run: `npm run test` or `npx astro check`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "feat: add branches category to slotr landing (EN)"
```

### Task 4: Update slotr.astro spans for new category

**Files:**
- Modify: `src/pages/slotr.astro:27-86` (ES categories)
- Modify: `src/pages/slotr.astro:96-155` (EN categories)

- [ ] **Step 1: Write the failing test**

```typescript
def test_slotr_category_spans_sum_to_24():
    import { featureCategories, featureCategoriesEn } from 'src/pages/slotr.astro'
    const esSum = featureCategories.reduce((sum, cat) => sum + cat.span, 0)
    const enSum = featureCategoriesEn.reduce((sum, cat) => sum + cat.span, 0)
    assert esSum === 24
    assert enSum === 24
    // Verify each category has span 4
    assert featureCategories.every(cat => cat.span === 4)
    assert featureCategoriesEn.every(cat => cat.span === 4)
```

- [ ] **Step 2: Run test to verify it fails**

Run: `npm run test` or `npx astro check`
Expected: FAIL with "Cannot find name 'featureCategories'"

- [ ] **Step 3: Write minimal implementation**

```typescript
// Update existing categories to span 4
const featureCategories: FeatureCategory[] = [
  {
    heading: 'Reservas',
    description: 'Todo para que tus clientes reserven fácil.',
    icon: 'calendar',
    span: 4,  // was 5
    features: [
      { icon: 'calendar', name: 'Reservas online', description: 'Página pública donde tus clientes reservan su turno sin llamar.' },
      { icon: 'list', name: 'Múltiples servicios', description: 'Servicios con duración y rango de precios. Con 10 o más servicios, los clientes navegan por categoría primero.' },
      { icon: 'link', name: 'Multi-servicios', description: 'Tus clientes pueden reservar varios servicios en una sola cita. El sistema calcula duración total y precio combinado automáticamente.' },
      { icon: 'folder', name: 'Categorías y precios', description: 'Organizá tus servicios por categoría y mostrá rangos de precio para que el cliente tenga una idea clara antes de reservar.' },
    ],
  },
  {
    heading: 'Gestión',
    description: 'Control total de tu equipo y tu agenda.',
    icon: 'grid',
    span: 4,  // was 7
    features: [
      { icon: 'grid', name: 'Gestión de agenda', description: 'Vista de calendario por recurso con bloqueos y cancelaciones.' },
      { icon: 'users', name: 'Staff y recursos', description: 'Soporte para personas y recursos físicos, con roles admin/staff y permisos granulares por módulo.' },
      { icon: 'settings', name: 'Panel administrativo', description: 'Configuración completa: horarios, servicios, bloqueos y ajustes del negocio.' },
      { icon: 'lock', name: 'Bloqueos con motivo', description: 'Bloqueá turnos individuales o días completos indicando el motivo. Visible en la agenda para todo el equipo.' },
      { icon: 'shield', name: 'Permisos granulares', description: 'Controlá quién ve y gestiona cada agenda. Permisos independientes por staff para agenda, bloqueos y configuración.' },
    ],
  },
  {
    heading: 'Comunicación',
    description: 'Mantené informados a tus clientes y a tu equipo.',
    icon: 'bell',
    span: 4,  // was 5
    features: [
      { icon: 'bell', name: 'Notificaciones', description: 'Avisos instantáneos por Telegram al staff cuando un cliente reserva. Integración con bot de Telegram para mantener al equipo informado en tiempo real.' },
      { icon: 'mail', name: 'Confirmación por email', description: 'Tus clientes reciben un email con los detalles de su turno al confirmar la reserva.' },
      { icon: 'clock', name: 'Recordatorios automáticos', description: 'Emails de recordatorio enviados automáticamente antes del turno para reducir ausencias.' },
      { icon: 'messageCircle', name: 'Confirmación por WhatsApp', description: 'Botón directo en la pantalla de confirmación para que el cliente envíe los datos de su turno por WhatsApp.' },
    ],
  },
  {
    heading: 'Marketing',
    description: 'Atraé más clientes y fidelizá a los que ya tenés.',
    icon: 'sparkles',
    span: 4,  // was 4 (unchanged)
    isNew: true,
    features: [
      { icon: 'sparkles', name: 'Eventos y Promociones', description: 'Creá promociones con descuentos porcentuales o fijos, notificaciones visuales con íconos y banners de color. Solo un evento activo a la vez. Tus clientes ven las ofertas directamente en la página de reservas.' },
      { icon: 'star', name: 'Reseñas de clientes', description: 'Los clientes califican su experiencia con estrellas y texto. El puntaje promedio y las reseñas recientes se muestran en tu página pública.' },
    ],
  },
  {
    heading: 'Analytics',
    description: 'Datos claros para tomar mejores decisiones.',
    icon: 'activity',
    span: 4,  // was 3
    features: [
      { icon: 'activity', name: 'Dashboard de métricas', description: 'KPIs de turnos e ingresos estimados, 5 gráficos por período (7/30/90 días), ranking de servicios, franjas horarias pico y clientes frecuentes.' },
      { icon: 'palette', name: 'Personalización', description: '16 paletas de color, logo propio y etiquetas configurables. Tu sistema de turnos con tu identidad visual.' },
    ],
  },
  // Sucursales category inserted here (span 4)
];
```

- [ ] **Step 4: Run test to verify it passes**

Run: `npm run test` or `npx astro check`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "feat: rebalancear spans de categorías para nueva sucursales"
```

### Task 5: Update slotr.astro EN spans for new category

**Files:**
- Modify: `src/pages/slotr.astro:96-155` (EN categories)

- [ ] **Step 1: Write the failing test**

```typescript
def test_slotr_category_spans_en_sum_to_24():
    import { featureCategoriesEn } from 'src/pages/slotr.astro'
    const enSum = featureCategoriesEn.reduce((sum, cat) => sum + cat.span, 0)
    assert enSum === 24
    assert featureCategoriesEn.every(cat => cat.span === 4)
```

- [ ] **Step 2: Run test to verify it fails**

Run: `npm run test` or `npx astro check`
Expected: FAIL with "Cannot find name 'featureCategoriesEn'"

- [ ] **Step 3: Write minimal implementation**

```typescript
// Update existing EN categories to span 4
const featureCategoriesEn: FeatureCategory[] = [
  {
    heading: 'Bookings',
    description: 'Everything so your clients can book easily.',
    icon: 'calendar',
    span: 4,  // was 5
    features: [
      { icon: 'calendar', name: 'Online bookings', description: 'Public page where your clients book their appointment without calling.' },
      { icon: 'list', name: 'Multiple services', description: 'Services with duration and price range. With 10 or more services, clients browse by category first.' },
      { icon: 'link', name: 'Multi-services', description: 'Your clients can book multiple services in a single appointment. The system calculates total duration and combined price automatically.' },
      { icon: 'folder', name: 'Categories and prices', description: 'Organize your services by category and display price ranges so clients have a clear idea before booking.' },
    ],
  },
  {
    heading: 'Management',
    description: 'Total control of your team and schedule.',
    icon: 'grid',
    span: 4,  // was 7
    features: [
      { icon: 'grid', name: 'Schedule management', description: 'Calendar view by resource with blocks and cancellations.' },
      { icon: 'users', name: 'Staff and resources', description: 'Support for people and physical resources, with admin/staff roles and granular permissions per module.' },
      { icon: 'settings', name: 'Admin panel', description: 'Full configuration: hours, services, blocks and business settings.' },
      { icon: 'lock', name: 'Blocks with reason', description: 'Block individual slots or full days indicating the reason. Visible on the schedule for the entire team.' },
      { icon: 'shield', name: 'Granular permissions', description: 'Control who sees and manages each schedule. Independent permissions per staff for schedule, blocks and configuration.' },
    ],
  },
  {
    heading: 'Communication',
    description: 'Keep your clients and team informed.',
    icon: 'bell',
    span: 4,  // was 5
    features: [
      { icon: 'bell', name: 'Notifications', description: 'Instant Telegram alerts to staff when a client books. Telegram bot integration to keep the team informed in real time.' },
      { icon: 'mail', name: 'Email confirmation', description: 'Your clients receive an email with their appointment details upon confirming the booking.' },
      { icon: 'clock', name: 'Automatic reminders', description: 'Reminder emails sent automatically before the appointment to reduce no-shows.' },
      { icon: 'messageCircle', name: 'WhatsApp confirmation', description: 'Direct button on the confirmation screen so the client can send their appointment details via WhatsApp.' },
    ],
  },
  {
    heading: 'Marketing',
    description: 'Attract more clients and retain the ones you have.',
    icon: 'sparkles',
    span: 4,  // was 4 (unchanged)
    isNew: true,
    features: [
      { icon: 'sparkles', name: 'Events & Promotions', description: 'Create promotions with percentage or fixed discounts, visual notifications with icons and color banners. Only one active event at a time. Your clients see offers directly on the booking page.' },
      { icon: 'star', name: 'Client reviews', description: 'Clients rate their experience with stars and text. The average score and recent reviews are shown on your public page.' },
    ],
  },
  {
    heading: 'Analytics',
    description: 'Clear data to make better decisions.',
    icon: 'activity',
    span: 4,  // was 3
    features: [
      { icon: 'activity', name: 'Metrics dashboard', description: 'KPIs of appointments and estimated revenue, 5 charts by period (7/30/90 days), service ranking, peak time slots and frequent clients.' },
      { icon: 'palette', name: 'Customization', description: '16 color palettes, custom logo and configurable labels. Your appointment system with your visual identity.' },
    ],
  },
  // Branches category inserted here (span 4)
];
```

- [ ] **Step 4: Run test to verify it passes**

Run: `npm run test` or `npx astro check`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "feat: rebalancear spans de categorías EN para nueva sucursales"
```

### Task 6: Run build and verify page renders

**Files:**
- No file changes
- Test: `npx astro build` (or `npm run build`)

- [ ] **Step 1: Run build**

```bash
npm run build
```

- [ ] **Step 2: Verify build output**

Check that `dist/` directory contains the slotr page and no TypeScript errors

- [ ] **Step 3: Verify page renders**

```bash
# Quick check for slotr page in dist
ls dist/ | grep -i slotr
```

- [ ] **Step 4: Commit**

```bash
git commit -m "chore: build después de agregar sucursales"
```

---

## Self-Review

After writing the complete plan, look at the spec with fresh eyes and check the plan against it. This is a checklist you run yourself — not a subagent dispatch.

**1. Spec coverage:** Skim each section/requirement in the spec. Can you point to a task that implements it? List any gaps.

✅ **Layout:** Task 2 & 3 add Sucursales category with span 4, inserted in position 3
✅ **Content:** Task 2 & 3 add ES and EN category content with 4 features each
✅ **Icons:** Task 1 adds building and mapPin icons
✅ **Spans:** Task 4 & 5 rebalance all categories to span 4 (24 total)
✅ **Files:** All 3 files to modify are covered (icons.ts, slotr.astro ES, slotr.astro EN)
✅ **Validation:** Task 6 runs build and verifies page renders
✅ **No placeholders:** All steps contain actual code, commands, and expected outputs
✅ **Type consistency:** FeatureCategory type is used consistently across all tasks

**2. Placeholder scan:** Search the plan for red flags. None found.

**3. Type consistency:** All references to `featureCategories` and `featureCategoriesEn` match the spec. The `FeatureCategory` type is defined in the existing slotr.astro and used consistently.

---

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2026-06-11-slotr-landing-sucursales-plan.md`. Two execution options:

**1. Subagent-Driven (recommended)** - I dispatch a fresh subagent per task, review between tasks, fast iteration

**2. Inline Execution** - Execute tasks in this session using executing-plans, batch execution with checkpoints

**Which approach?**

**If Subagent-Driven chosen:**
- **REQUIRED SUB-SKILL:** Use superpowers:subagent-driven-development
- Fresh subagent per task + two-stage review

**If Inline Execution chosen:**
- **REQUIRED SUB-SKILL:** Use superpowers:executing-plans
- Batch execution with checkpoints for review
