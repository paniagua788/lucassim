# lucassim.com — Diseño del sitio web

**Fecha:** 2026-03-24
**Estado:** Aprobado

---

## Resumen

Sitio web público de presentación para lucassim, desarrollador independiente paraguayo. El objetivo es tener un destino central donde potenciales clientes puedan conocer quién es Lucas y explorar sus dos productos SaaS: VareApp y Slotr. Cada producto tiene su propia página de aterrizaje para facilitar el proceso de venta.

---

## Decisiones de arquitectura

| Decisión | Elección | Motivo |
|---|---|---|
| Framework | Astro | Genera HTML estático, ideal para sitios de presentación. Permite componentes reutilizables sin costo de hosting extra. |
| Hosting | Netlify / Cloudflare Pages / GitHub Pages | Gratis para sitios estáticos. |
| Estructura | Un solo repo, tres páginas | `/`, `/vareapp`, `/slotr`. Simple de mantener, sin subdominios. |
| Estilo visual | Dark / Minimalista | Fondo negro, tipografía limpia. Acentos naranja para VareApp, violeta para Slotr. |

---

## Páginas

### 1. Home — `lucassim.com/`

Página principal. Presenta al desarrollador y lista los dos productos.

#### Secciones

**Navbar**
- Logo "lucassim" (izquierda), con `href="/"`
- Links: "Proyectos" (scroll `#productos`) y "Contacto" (scroll `#contacto`)
- Fijo en el top
- `showBack: false` — muestra los links de navegación normales

**Hero**
- Título: "Hola, soy Lucas. Ingeniero de Sistemas."
- Bio breve: más de 5 años de experiencia, proactivo, orientado al crecimiento, apasionado por construir productos que resuelvan problemas reales.
- Subtítulo: "Desarrollo soluciones diseñadas para el mercado paraguayo — simples, funcionales y listas para escalar."
- CTAs: "Ver proyectos ↓" (scroll) y "Contacto"

**Productos**
- Dos tarjetas lado a lado:
  - **VareApp** (fondo oscuro con acento naranja): tagline, 4 features clave en lista, botón "Ver VareApp →" → `/vareapp`
  - **Slotr** (fondo oscuro con acento violeta): tagline, 4 features clave en lista, botón "Ver Slotr →" → `/slotr`

**Contacto**
- Título: "¿Hablamos?"
- Subtítulo: "Si te interesa alguno de los productos o tenés una consulta, escribime directamente."
- Botones: WhatsApp (`https://wa.me/XXXXXXXXX`) y Email (`mailto:XXXXXXXXX`) — placeholders hasta tener los datos reales

**Footer**
- Logo lucassim (izquierda), con `href="/"`
- Links sociales: GitHub, LinkedIn, Twitter/X (centro). Mientras no se tengan las URLs reales, los íconos se renderizan con `href="#"` y `aria-disabled="true"` (visualmente presentes pero no funcionales).
- Copyright © lucassim (derecha)
- En páginas de producto: se agrega link "← Volver al inicio" con `href="/"`. Controlado con prop `showHomeLink: boolean` en `Footer.astro`.

---

### 2. VareApp — `lucassim.com/vareapp`

Página de aterrizaje dedicada a VareApp.

#### Secciones

**Navbar**
- Logo "lucassim" con `href="/"`
- "← Volver" con `href="/"` (derecha)
- `showBack: true` — oculta los links de navegación normales y muestra solo el link de regreso

**Hero**
- Eyebrow: "SaaS · Gastronomía"
- Título: "VareApp"
- Tagline: "Menú digital y sistema de gestión de pedidos para restaurantes, cafeterías y food trucks."
- CTA: botón único "Consultá por una demo" → `https://wa.me/XXXXXXXXX` (WhatsApp, canal prioritario)
- Fondo con degradado sutil naranja oscuro

**Funcionalidades**
Grid 2 columnas × 3 filas con las 6 features principales:
1. **Menú digital** — Catálogo con categorías, variantes, extras y fotos.
2. **Gestión de pedidos** — Pedidos en tiempo real con notificación por WhatsApp.
3. **Panel administrativo** — Control total: productos, horarios, staff y configuración.
4. **Caja** — Registro de ventas, impresión de tickets y facturas electrónicas habilitadas por la DNIT.
5. **Inventario** — Control de stock con alertas de bajo inventario.
6. **Métricas** — Dashboard con ventas, productos top y horas pico.

**¿Para quién es?**
- Título: "Ideal para negocios gastronómicos"
- Chips de tipos de negocio: Restaurantes, Cafeterías, Food trucks, Rotiserías, + "Cualquier negocio con menú y pedidos"

**Planes**
Dos planes lado a lado, ambos con "Consultá por el precio":

| | Esencial | Pro |
|---|---|---|
| Menú digital | ✓ | ✓ |
| Gestión de pedidos | ✓ | ✓ |
| Panel admin | ✓ | ✓ |
| Caja — registro de ventas | ✓ | ✓ |
| Impresión de ticket* | ✓ | ✓ |
| Factura electrónica (DNIT) | ✕ | ✓ |
| Inventario | ✕ | ✓ |
| Métricas avanzadas | ✕ | ✓ |

*El ticket del plan Esencial no tiene valor fiscal.
La factura electrónica del plan Pro tiene plena validez fiscal habilitada por la DNIT.

**CTA final**
- Título: "¿Listo para digitalizar tu negocio?"
- Subtítulo: "Escribime y coordinamos una demo personalizada."
- Botones: WhatsApp y Email

**Footer**
- Igual al del home. Link "← Volver al inicio".

---

### 3. Slotr — `lucassim.com/slotr`

Página de aterrizaje dedicada a Slotr.

#### Secciones

**Navbar**
- Logo "lucassim" con `href="/"`
- "← Volver" con `href="/"` (derecha)
- `showBack: true` — oculta los links de navegación normales y muestra solo el link de regreso

**Hero**
- Eyebrow: "SaaS · Agendamiento"
- Título: "Slotr"
- Tagline: "Sistema de turnos online para clínicas, peluquerías, consultoras y canchas deportivas."
- CTA: botón único "Consultá por una demo" → `https://wa.me/XXXXXXXXX` (WhatsApp, canal prioritario)
- Fondo con degradado sutil violeta oscuro

**Funcionalidades**
Grid 2 columnas × 3 filas con las 6 features principales:
1. **Reservas online** — Página pública donde los clientes reservan su turno.
2. **Gestión de agenda** — Vista de calendario por recurso con bloqueos y cancelaciones.
3. **Múltiples servicios** — Configuración de servicios con duración y disponibilidad.
4. **Staff y recursos** — Soporte para personas (peluqueros, profesionales) y recursos físicos (canchas, consultorios).
5. **Notificaciones** — Avisos automáticos al momento de la reserva.
6. **Panel administrativo** — Configuración completa: horarios, servicios, bloqueos, ajustes.

**¿Para quién es?**
- Título: "Para cualquier negocio que trabaje con turnos"
- Chips: Clínicas, Peluquerías, Consultoras, Canchas deportivas, Consultorios, + "Cualquier negocio que agenda citas"

**Precios**
Modelo por volumen de recursos (calendarios). Sin precios fijos — "Consultá".

Tres rangos con ejemplos de uso real:

| Rango | Ejemplo | Precio |
|---|---|---|
| 1 recurso | Consultorio individual, peluquero solo | Consultá |
| 2–3 recursos | 3 canchas de pádel, 2 profesionales | Consultá |
| 4+ recursos | Clínica con múltiples especialistas | Consultá |

Nota: el precio base incluye 1 recurso/calendario. Cada recurso adicional tiene un costo adicional.

**CTA final**
- Título: "¿Querés que tus clientes reserven solos?"
- Subtítulo: "Escribime y te muestro cómo funciona."
- Botones: WhatsApp y Email

**Footer**
- Igual al del home. Link "← Volver al inicio".

---

## Componentes reutilizables (Astro)

| Componente | Props | Usado en |
|---|---|---|
| `Navbar.astro` | `showBack: boolean` — si `true`, oculta los links de navegación y muestra solo "← Volver" con `href="/"` | Todas las páginas |
| `Footer.astro` | `showHomeLink: boolean` — si `true`, agrega link "← Volver al inicio" con `href="/"` | Todas las páginas |
| `ContactButtons.astro` | `whatsapp: string` (URL completa `https://wa.me/...`), `email: string` (dirección sin `mailto:` — el componente antepone `mailto:` internamente) | Home (sección contacto) + CTA final de cada producto |
| `FeatureCard.astro` | `icon: string`, `name: string`, `description: string` | Páginas de producto (grid de funcionalidades) |
| `ProductCard.astro` | `name`, `tagline`, `accent`, `features[]`, `href` | Home (sección productos) |

---

## Estilo y tokens de diseño

- **Fondo base:** `#111111`
- **Superficies de tarjetas:** `#161616`, `#1a1a1a`
- **Texto primario:** `#ffffff`
- **Texto secundario:** `#888888`, `#555555`
- **Acento VareApp:** `#f97316` (orange-500)
- **Acento Slotr:** `#7c3aed` (violet-600)
- **Bordes:** `#2a2a2a`
- **Tipografía:** Inter (o similar — sans-serif del sistema como fallback)
- **Bordes redondeados:** `8px` tarjetas internas, `12px` bloques principales

---

## Contenido pendiente a completar

Los siguientes datos deben ser provistos antes del deploy:

- [ ] WhatsApp de contacto — reemplazar `XXXXXXXXX` en todos los `https://wa.me/XXXXXXXXX`
- [ ] Email de contacto — reemplazar `XXXXXXXXX` en todos los `mailto:XXXXXXXXX`
- [ ] Links reales de GitHub, LinkedIn, Twitter/X — mientras tanto se renderizan con `href="#"` y `aria-disabled="true"`
- [ ] Precios (opcionales — el sitio puede lanzar sin ellos con "Consultá")
- [ ] Screenshots de los productos (marcado como feature futura)

---

## Fuera de alcance (v1)

- Testimonios de clientes (se agrega cuando haya clientes reales)
- Sección "Sobre mí" extendida (la presentación queda solo en el Hero)
- Screenshots / demos interactivas
- Formulario de contacto con backend (se usa WhatsApp y email directo)
- Blog o sección de novedades
