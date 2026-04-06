# Portfolio Page — Design Spec

**Date:** 2026-04-06  
**Route:** `/portfolio`  
**Goal:** Página de portfolio profesional para enviar a reclutadores, con todo el contenido del CV de Lucas S. Paniagua.

---

## Contexto

Sitio estático Astro 6 + Tailwind CSS 4, hosteado en Cloudflare Pages. La página debe seguir siendo estática (sin SSR) pero puede usar JS en el cliente (compatible con Cloudflare Pages) para el toggle de idioma.

---

## Arquitectura

### Archivo principal
`src/pages/portfolio.astro` — usa `BaseLayout` con title y description propios.

### Componentes nuevos (`src/components/portfolio/`)
| Componente | Responsabilidad |
|---|---|
| `PortfolioHero.astro` | Nombre, roles, bio, contacto, toggle ES/EN |
| `SkillsGrid.astro` | Grilla de habilidades técnicas por categoría |
| `ExperienceList.astro` | Timeline de experiencia profesional (cronológico inverso) |
| `ProjectsList.astro` | Proyectos propios con stack tags |
| `EducationCerts.astro` | Educación y certificaciones en dos columnas |

### Toggle de idioma
- Un `<script>` vanilla en `portfolio.astro`
- Alterna clase `hidden` entre bloques con atributo `data-lang="es"` y `data-lang="en"`
- Estado inicial: español
- Pill style: `[ES] [EN]` en el header, top-right

---

## Estructura de secciones (orden)

1. **Hero** — Nombre, roles, resumen bio, botones de contacto, toggle ES/EN
2. **Habilidades técnicas** — Lo más relevante para reclutadores
3. **Experiencia profesional** — Timeline, cronológico inverso
4. **Proyectos propios** — VareApp, Slotr, MedicFile, Herramientas de Infraestructura
5. **Educación + Certificaciones** — Dos columnas desktop, stack mobile

---

## Diseño visual

El portfolio tiene su propio tema claro, **independiente** de los tokens oscuros del resto del sitio (`global.css` no se modifica).

### Paleta (clases Tailwind estándar)
| Uso | Clase |
|---|---|
| Fondo general | `bg-gray-50` |
| Cards / secciones | `bg-white border border-gray-200 rounded-xl` |
| Texto principal | `text-gray-900` |
| Texto secundario | `text-gray-500` |
| Acento (links, fechas) | `text-blue-600` |
| Tags de tecnología | `bg-blue-50 text-blue-700 rounded text-sm` |
| Toggle activo | `bg-gray-900 text-white rounded` |
| Toggle inactivo | `text-gray-500` |

### Hero
- Nombre: `text-4xl font-black text-gray-900`
- Roles: badges en línea separados por `·`
- Bio en `text-gray-600 max-w-2xl`
- Botones de contacto: WhatsApp (verde), Email (gris), LinkedIn (azul)
- Toggle ES/EN pill en esquina superior derecha

### Habilidades técnicas
- Grid de cards por categoría: Backend, Frontend, Bases de datos, DevOps/Cloud, Automatización, Infraestructura, ITSM & Gestión, Metodologías
- Cada card: título de categoría en `font-semibold text-gray-900` + tags de tecnologías en pills `bg-gray-100`

### Experiencia profesional
- Línea vertical izquierda: `border-l-2 border-gray-200`
- Cada entry: empresa (negrita), rol, fechas (`text-gray-500 text-sm`), bullets de logros
- 4 posiciones: Parque Tecnológico Itaipú (Feb 2025–Presente), Itaipú Binacional x2, Técnico de Redes

### Proyectos propios
- Cards con: nombre, descripción corta, stack tags coloreados, bullets de features clave
- Proyectos: VareApp, Slotr, MedicFile, Herramientas de Infraestructura & APIs

### Educación + Certificaciones
- Dos columnas en `sm:grid-cols-2`, stack en mobile
- Educación: título, institución
- Certificaciones agrupadas por categoría: Cloud & Infraestructura, Gestión de Servicios TI, Desarrollo & Metodologías, Seguridad

---

## Contenido bilingüe

Todo el texto de la página se escribe en dos bloques hermanos con `data-lang="es"` y `data-lang="en"`. El script oculta/muestra según el toggle. Los componentes reciben props para ambos idiomas o se duplican internamente.

**Estrategia elegida:** secciones duplicadas con `data-lang="es"` / `data-lang="en"` dentro de cada componente. El script vanilla oculta/muestra con `hidden`. Es la opción más simple, sin pasar estado desde el cliente a Astro (que es server-side).

---

## Navbar en la página de portfolio

Usa `<Navbar showBack={true} />` — solo muestra "← Volver" al home. El toggle de idioma vive dentro del hero, no en el navbar.

---

## Restricciones

- No modificar `global.css` ni los tokens existentes del sitio
- No crear `tailwind.config.mjs`
- No usar frameworks JS (React, Vue, etc.)
- El único JS es el script vanilla del toggle de idioma
- Compatible con `npm run build` sin errores como criterio de corrección

---

## Datos de contacto

```
WhatsApp: https://wa.me/595993294266
Email: lucas_paniagua@hotmail.com
LinkedIn: https://linkedin.com/in/paniagua788
Ubicación: Hernandarias, Paraguay
```
