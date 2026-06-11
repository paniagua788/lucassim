# Spec: Slotr Landing — Categoría Sucursales (multi-branch)

**Date:** 2026-06-11
**Status:** Approved

---

## Problem

El feature multi-sucursal ya está implementado y activo en el backend de Slotr (spec original en `~/Documentos/Projects/turnosApp/docs/superpowers/specs/2026-06-10-multi-branch-design.md`, commits `5ba8049`→`f286bf6`). Sin embargo, la landing page pública de Slotr (`/slotr` en lucassim.com.py) no refleja esta capacidad. Un negocio con varias ubicaciones físicas que visita la landing no encuentra evidencia de que Slotr soporte ese caso de uso.

---

## Solution

Agregar una nueva categoría "Sucursales" al bento grid de features en `src/pages/slotr.astro`, marcada con badge "Nuevo" (igual que la categoría "Marketing"). Insertar 4 features que destaquen los beneficios comerciales clave del multi-branch. Rebalancear los spans de las 5 categorías existentes de 5+7+5+4+3 (24 pts, 2 filas) a un layout de 6 cards iguales a span 4 cada una (24 pts, 2 filas balanceadas).

**Por qué rebalancear y no añadir una 3ª fila:** mantiene el ritmo visual actual (2 filas, 12 cols cada una), evita crear una "isla" destacada de un solo card, y la presencia del badge "Nuevo" ya da la prominencia necesaria al feature.

### Goals
- Reflejar el feature multi-branch en la landing de Slotr
- Mantener el patrón visual de bento grid (2 filas, 12 cols)
- Card con badge "Nuevo" consistente con cómo se presentó "Marketing"
- Contenido bilingüe (ES + EN) simétrico
- Sin cambios de comportamiento runtime (sigue siendo 100% estático)

### Non-Goals
- Hero, secciones de pricing, target o contact del slotr.astro
- Cualquier feature nuevo de backend
- Imágenes / screenshots / mockups de la UI admin
- Sección expandida propia para el feature (todo entra en la grilla bento)
- Cambios en otras landings (`index.astro`, `vareapp.astro`, `portfolio.astro`)

---

## Design

### Layout del bento grid

**Actual** (5 cards, 2 filas de 12 cols):

```
Row 1: Reservas(5)  + Gestión(7)                     = 12
Row 2: Comunicación(5) + Marketing(4) + Analytics(3) = 12
```

**Nuevo** (6 cards, 2 filas de 12 cols):

```
Row 1: Reservas(4) + Gestión(4) + Sucursales(4)      = 12   ← nueva, badge "Nuevo"
Row 2: Comunicación(4) + Marketing(4) + Analytics(4) = 12
```

Sucursales se inserta en posición 3 del array (entre Gestión y Comunicación), en la primera fila. El orden del array determina el orden visual.

### Rebalanceo de spans

| Categoría | Span antes | Span después |
|---|---|---|
| Reservas | 5 | 4 |
| Gestión | 7 | 4 |
| Comunicación | 5 | 4 |
| Marketing | 4 | 4 (sin cambio) |
| Analytics | 3 | 4 |
| **Sucursales** | — | 4 (nueva) |

### Contenido de la nueva categoría

**ES:**

```ts
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
}
```

**EN:**

```ts
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
}
```

### Iconos nuevos en `src/components/icons.ts`

Agregar dos íconos Lucide al objeto `icons` (manteniendo el patrón existente: `viewBox="0 0 24 24"`, `stroke="currentColor"`, `stroke-width="1.5"`, `stroke-linecap="round"`, `stroke-linejoin="round"`, `fill="none"`):

- **`building`**: edificio de 3 pisos (lucide `building-2`)
- **`mapPin`**: marcador de mapa (lucide `map-pin`)

El tipo `IconName` se actualiza automáticamente porque se deriva de `keyof typeof icons` (no requiere cambio explícito).

---

## Files to Modify

| Archivo | Cambio |
|---|---|
| `src/components/icons.ts` | Agregar entradas `building` y `mapPin` al objeto `icons` |
| `src/pages/slotr.astro` | (1) Reducir spans: Reservas 5→4, Gestión 7→4, Comunicación 5→4, Analytics 3→4. (2) Insertar nueva categoría Sucursales(span 4, isNew: true) en posición 3 del array `featureCategories` y en la misma posición de `featureCategoriesEn`. |

**NO se modifican:** `src/components/CategoryCard.astro` (ya soporta `isNew`, `isNewLabel` y `span` 1-12), `src/components/Navbar.astro`, `src/components/Footer.astro`, `src/components/ContactButtons.astro`, `src/components/ProductCard.astro`, `src/components/vareapp-icons.ts`, `src/layouts/BaseLayout.astro`, `src/styles/global.css`, otras páginas.

---

## Validation

- `npm run build` debe pasar sin errores de TypeScript
- La página `/slotr` debe renderizar 6 cards (5 existentes + Sucursales)
- En ES y EN: Sucursales/Branches visible con badge "Nuevo"/"New" (CategoríaCard usa `isNewLabel="New"` en EN, default "Nuevo" en ES — manejado en el template actual, sin cambios)
- Layout responsive: en mobile todas las cards a 1 col (`grid-cols-1`); en lg+ 2 filas balanceadas
- Hover/animaciones del bento grid: sin cambios
- `prefers-reduced-motion`: sigue desactivando animaciones del hero (no afectado)
- Lenguaje del toggle: ES sigue siendo el idioma por defecto, EN se muestra vía `[data-lang]` (sin cambios)
- Sin regresiones en las otras 5 categorías: cada una mantiene su icono, heading, descripción, features originales

---

## Out of Scope

- Cambios a otras landings (`index.astro`, `vareapp.astro`, `portfolio.astro`)
- Refactor de la estructura de `featureCategories` a un helper compartido entre ES/EN
- Agregar un card "sucursales" también en `index.astro` o en `ProductCard.astro` (queda como follow-up si el usuario lo pide)
- Capturas de pantalla o mockups del admin panel mostrando la sección Sucursales
- Animación especial para cards con `isNew` (Marketing tampoco la tiene — se mantiene la convención)
- Documentar el feature en README o AGENTS.md
- Cambios al backend de Slotr (multi-branch ya está implementado, ver spec origen)
