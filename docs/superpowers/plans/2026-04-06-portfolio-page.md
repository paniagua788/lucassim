# Portfolio Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Crear la página `/portfolio` — portfolio profesional bilingüe (ES/EN) con tema claro, construida en Astro 6 + Tailwind CSS, sin frameworks JS, con toggle de idioma vanilla.

**Architecture:** Página estática `src/pages/portfolio.astro` que ensambla 5 componentes bajo `src/components/portfolio/`. Todo el contenido bilingüe usa el patrón `data-lang="es"` / `data-lang="en"` con un script vanilla que alterna `hidden`. El tema claro se aísla dentro de un `<div class="bg-gray-50 text-gray-900 min-h-screen">` para no afectar el resto del sitio.

**Tech Stack:** Astro 6, Tailwind CSS 4 (clases estándar, sin modificar `global.css`), JS vanilla mínimo (solo el toggle).

**Verificación:** `npm run build` sin errores es el equivalente de los tests (no hay test suite).

---

## File Map

| Acción | Archivo |
|---|---|
| Crear | `src/components/portfolio/PortfolioNavbar.astro` |
| Crear | `src/components/portfolio/PortfolioHero.astro` |
| Crear | `src/components/portfolio/SkillsGrid.astro` |
| Crear | `src/components/portfolio/ExperienceList.astro` |
| Crear | `src/components/portfolio/ProjectsList.astro` |
| Crear | `src/components/portfolio/EducationCerts.astro` |
| Crear | `src/pages/portfolio.astro` |

---

## Task 1: PortfolioNavbar component

**Files:**
- Create: `src/components/portfolio/PortfolioNavbar.astro`

- [ ] **Step 1: Crear el componente**

```astro
---
// src/components/portfolio/PortfolioNavbar.astro
// Navbar light con toggle de idioma para la página portfolio.
// Sin props — los botones del toggle son manejados por el script en portfolio.astro.
---

<nav class="fixed top-0 left-0 right-0 z-50 border-b border-gray-200 bg-white/90 backdrop-blur-sm">
  <div class="max-w-4xl mx-auto px-6 h-14 flex items-center justify-between">
    <a href="/" class="text-sm font-bold tracking-widest uppercase text-gray-900 hover:text-gray-600 transition-colors">
      lucassim
    </a>

    <div class="flex items-center gap-4">
      <!-- Lang toggle -->
      <div class="flex gap-1 p-1 bg-gray-100 rounded-lg">
        <button
          data-lang-btn
          data-target="es"
          class="px-3 py-1 text-xs font-semibold rounded-md bg-gray-900 text-white transition-colors"
        >
          ES
        </button>
        <button
          data-lang-btn
          data-target="en"
          class="px-3 py-1 text-xs font-semibold rounded-md text-gray-500 transition-colors"
        >
          EN
        </button>
      </div>

      <a href="/" class="text-sm text-gray-500 hover:text-gray-900 transition-colors">
        ← Volver
      </a>
    </div>
  </div>
</nav>

<!-- Spacer para compensar la navbar fixed -->
<div class="h-14"></div>
```

- [ ] **Step 2: Verificar build**

```bash
npm run build
```

Esperado: sin errores. (El componente no está importado aún — Astro no lo compila en soledad, OK si muestra 0 páginas nuevas.)

- [ ] **Step 3: Commit**

```bash
git add src/components/portfolio/PortfolioNavbar.astro
git commit -m "feat: add PortfolioNavbar component with lang toggle"
```

---

## Task 2: PortfolioHero component

**Files:**
- Create: `src/components/portfolio/PortfolioHero.astro`

- [ ] **Step 1: Crear el componente**

```astro
---
// src/components/portfolio/PortfolioHero.astro
// Hero del portfolio: nombre, roles, bio, contacto. Bilingüe con data-lang.
---

<!-- ESPAÑOL -->
<section data-lang="es" class="py-16 px-6 max-w-4xl mx-auto">
  <p class="text-xs text-gray-400 uppercase tracking-widest mb-3">Hernandarias, Paraguay</p>

  <h1 class="text-4xl sm:text-5xl font-black text-gray-900 mb-3">
    Lucas S. Paniagua
  </h1>

  <div class="flex flex-wrap gap-2 mb-6">
    <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-xs font-semibold">Full-Stack Developer</span>
    <span class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold">System Administrator</span>
    <span class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold">Support Engineer</span>
    <span class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold">Inglés C1</span>
  </div>

  <p class="text-gray-600 max-w-2xl leading-relaxed mb-8">
    Ingeniero de Sistemas con más de 5 años de experiencia que combina desarrollo de software con
    una base sólida en infraestructura, redes y gestión de servicios TI. Especializado en Python
    (Flask, FastAPI, Django), JavaScript/TypeScript y APIs REST, con proyectos SaaS propios en
    producción. Background en soporte empresarial de alta demanda (500+ usuarios, uptime &gt;99.5%),
    ITSM con ServiceNow (3+ años), certificación ITIL 4 y AWS Cloud Practitioner. Combina mentalidad
    de producto con capacidad de operar en entornos críticos. Scrum certificado, autodidacta y
    orientado a la mejora continua.
  </p>

  <div class="flex flex-wrap gap-3">
    <a
      href="https://wa.me/595993294266"
      target="_blank"
      rel="noopener noreferrer"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold bg-green-600 text-white hover:bg-green-700 transition-colors"
    >
      WhatsApp
    </a>
    <a
      href="mailto:lucas_paniagua@hotmail.com"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold border border-gray-300 text-gray-700 hover:border-gray-500 hover:text-gray-900 transition-colors"
    >
      Email
    </a>
    <a
      href="https://linkedin.com/in/paniagua788"
      target="_blank"
      rel="noopener noreferrer"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold bg-blue-600 text-white hover:bg-blue-700 transition-colors"
    >
      LinkedIn
    </a>
    <a
      href="https://lucassim.com.py"
      target="_blank"
      rel="noopener noreferrer"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold border border-gray-300 text-gray-700 hover:border-gray-500 hover:text-gray-900 transition-colors"
    >
      lucassim.com.py ↗
    </a>
  </div>
</section>

<!-- ENGLISH -->
<section data-lang="en" class="hidden py-16 px-6 max-w-4xl mx-auto">
  <p class="text-xs text-gray-400 uppercase tracking-widest mb-3">Hernandarias, Paraguay</p>

  <h1 class="text-4xl sm:text-5xl font-black text-gray-900 mb-3">
    Lucas S. Paniagua
  </h1>

  <div class="flex flex-wrap gap-2 mb-6">
    <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-xs font-semibold">Full-Stack Developer</span>
    <span class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold">System Administrator</span>
    <span class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold">Support Engineer</span>
    <span class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold">English C1</span>
  </div>

  <p class="text-gray-600 max-w-2xl leading-relaxed mb-8">
    Systems Engineer with 5+ years of experience combining software development with a solid
    foundation in infrastructure, networking, and IT service management. Specialized in Python
    (Flask, FastAPI, Django), JavaScript/TypeScript, and REST APIs, with own SaaS projects in
    production. Background in high-demand enterprise support (500+ users, uptime &gt;99.5%),
    ITSM with ServiceNow (3+ years), ITIL 4 certified, and AWS Cloud Practitioner. Combines a
    product mindset with the ability to operate in critical environments. Scrum certified,
    self-taught, and committed to continuous improvement.
  </p>

  <div class="flex flex-wrap gap-3">
    <a
      href="https://wa.me/595993294266"
      target="_blank"
      rel="noopener noreferrer"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold bg-green-600 text-white hover:bg-green-700 transition-colors"
    >
      WhatsApp
    </a>
    <a
      href="mailto:lucas_paniagua@hotmail.com"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold border border-gray-300 text-gray-700 hover:border-gray-500 hover:text-gray-900 transition-colors"
    >
      Email
    </a>
    <a
      href="https://linkedin.com/in/paniagua788"
      target="_blank"
      rel="noopener noreferrer"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold bg-blue-600 text-white hover:bg-blue-700 transition-colors"
    >
      LinkedIn
    </a>
    <a
      href="https://lucassim.com.py"
      target="_blank"
      rel="noopener noreferrer"
      class="px-5 py-2.5 rounded-lg text-sm font-semibold border border-gray-300 text-gray-700 hover:border-gray-500 hover:text-gray-900 transition-colors"
    >
      lucassim.com.py ↗
    </a>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/portfolio/PortfolioHero.astro
git commit -m "feat: add PortfolioHero component (bilingual)"
```

---

## Task 3: SkillsGrid component

**Files:**
- Create: `src/components/portfolio/SkillsGrid.astro`

- [ ] **Step 1: Crear el componente**

```astro
---
// src/components/portfolio/SkillsGrid.astro
// Grilla de habilidades técnicas por categoría. Bilingüe con data-lang.
---

<!-- ESPAÑOL -->
<section data-lang="es" class="py-12 px-6 max-w-4xl mx-auto">
  <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Habilidades Técnicas</h2>

  <div class="grid sm:grid-cols-2 gap-4">

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Backend</p>
      <div class="flex flex-wrap gap-1.5">
        {['Python', 'Flask', 'FastAPI', 'Django REST', 'Node.js / Express', 'REST APIs', 'async/await', 'SOLID', 'Clean Code', 'Pytest'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Frontend</p>
      <div class="flex flex-wrap gap-1.5">
        {['JavaScript', 'TypeScript', 'React', 'HTML5', 'CSS3', 'TailwindCSS', 'Jinja2'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Bases de datos</p>
      <div class="flex flex-wrap gap-1.5">
        {['PostgreSQL', 'MongoDB', 'MySQL', 'Redis', 'SQLAlchemy', 'PyMongo', 'Alembic'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">DevOps / Cloud</p>
      <div class="flex flex-wrap gap-1.5">
        {['Docker', 'AWS (S3, Lambda, API Gateway, EC2)', 'Azure', 'Heroku', 'CI/CD', 'Git & GitHub', 'Linux avanzado'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Automatización</p>
      <div class="flex flex-wrap gap-1.5">
        {['Python scripts', 'PowerShell', 'Webhooks', 'WhatsApp Cloud API', 'Telegram Bot API', 'Integración de APIs externas'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Infraestructura</p>
      <div class="flex flex-wrap gap-1.5">
        {['Active Directory', 'GPOs', 'Windows Server', 'Hyper-V', 'VMware', 'MECM', 'Sysprep/PXE', 'Redes TCP/IP', 'VLANs'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">ITSM & Gestión</p>
      <div class="flex flex-wrap gap-1.5">
        {['ServiceNow (3+ años, avanzado)', 'ITIL 4 Foundation', 'Jira', 'Confluence', 'SLAs/KPIs', 'Gestión de activos TI'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Metodologías</p>
      <div class="flex flex-wrap gap-1.5">
        {['Scrum (Certificado)', 'Kanban', 'Documentación técnica', 'ADRs', 'OpenAPI/Swagger'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

  </div>
</section>

<!-- ENGLISH -->
<section data-lang="en" class="hidden py-12 px-6 max-w-4xl mx-auto">
  <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Technical Skills</h2>

  <div class="grid sm:grid-cols-2 gap-4">

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Backend</p>
      <div class="flex flex-wrap gap-1.5">
        {['Python', 'Flask', 'FastAPI', 'Django REST', 'Node.js / Express', 'REST APIs', 'async/await', 'SOLID', 'Clean Code', 'Pytest'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Frontend</p>
      <div class="flex flex-wrap gap-1.5">
        {['JavaScript', 'TypeScript', 'React', 'HTML5', 'CSS3', 'TailwindCSS', 'Jinja2'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Databases</p>
      <div class="flex flex-wrap gap-1.5">
        {['PostgreSQL', 'MongoDB', 'MySQL', 'Redis', 'SQLAlchemy', 'PyMongo', 'Alembic'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">DevOps / Cloud</p>
      <div class="flex flex-wrap gap-1.5">
        {['Docker', 'AWS (S3, Lambda, API Gateway, EC2)', 'Azure', 'Heroku', 'CI/CD', 'Git & GitHub', 'Advanced Linux'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Automation</p>
      <div class="flex flex-wrap gap-1.5">
        {['Python scripts', 'PowerShell', 'Webhooks', 'WhatsApp Cloud API', 'Telegram Bot API', 'External API integration'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Infrastructure</p>
      <div class="flex flex-wrap gap-1.5">
        {['Active Directory', 'GPOs', 'Windows Server', 'Hyper-V', 'VMware', 'MECM', 'Sysprep/PXE', 'TCP/IP Networks', 'VLANs'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">ITSM & Management</p>
      <div class="flex flex-wrap gap-1.5">
        {['ServiceNow (3+ years, advanced)', 'ITIL 4 Foundation', 'Jira', 'Confluence', 'SLAs/KPIs', 'IT Asset Management'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

    <div class="bg-white border border-gray-200 rounded-xl p-5">
      <p class="text-sm font-semibold text-gray-900 mb-3">Methodologies</p>
      <div class="flex flex-wrap gap-1.5">
        {['Scrum (Certified)', 'Kanban', 'Technical documentation', 'ADRs', 'OpenAPI/Swagger'].map(t => (
          <span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded text-xs">{t}</span>
        ))}
      </div>
    </div>

  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/portfolio/SkillsGrid.astro
git commit -m "feat: add SkillsGrid component (bilingual)"
```

---

## Task 4: ExperienceList component

**Files:**
- Create: `src/components/portfolio/ExperienceList.astro`

- [ ] **Step 1: Crear el componente**

```astro
---
// src/components/portfolio/ExperienceList.astro
// Timeline de experiencia profesional (cronológico inverso). Bilingüe.
---

<!-- ESPAÑOL -->
<section data-lang="es" class="py-12 px-6 max-w-4xl mx-auto">
  <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-8">Experiencia Profesional</h2>

  <div class="relative pl-6 border-l-2 border-gray-200 flex flex-col gap-10">

    <!-- Parque Tecnológico Itaipú -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-blue-600 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Full-Stack Python Developer</p>
          <p class="text-sm text-blue-600 font-medium">Parque Tecnológico Itaipú</p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Feb 2025 – Presente</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Desarrollo de aplicaciones de escritorio especializadas en Python con PySide6/Qt Framework para sistemas de subestaciones eléctricas bajo el estándar IEC 61850.</li>
        <li>Implementación de arquitectura desacoplada con principios SOLID y capa de servicios (AppService) para comunicación Frontend/Backend.</li>
        <li>Construcción de interfaces visuales interactivas con validación de datos en tiempo real para entornos industriales de alta disponibilidad.</li>
        <li>Desarrollo de funcionalidades para configuración de IEDs (Intelligent Electronic Devices) garantizando interoperabilidad en ecosistemas de subestaciones.</li>
        <li>Documentación técnica de decisiones de arquitectura y procesos de calidad; colaboración ágil en equipo multidisciplinario.</li>
      </ul>
    </div>

    <!-- Itaipú Binacional - Mesa de Servicios -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-gray-400 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Analista de Soporte Remoto – Mesa de Servicios</p>
          <p class="text-sm text-gray-600 font-medium">Itaipú Binacional <span class="text-gray-400">(vía Datapar / STI S.A.)</span></p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Sep 2023 – Feb 2025</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Gestión intensiva de ServiceNow: ciclo completo de incidentes, problemas, cambios y solicitudes para +500 usuarios empresariales.</li>
        <li>Desarrollo de scripts PowerShell para consultas en Active Directory, reduciendo tiempos de resolución de incidentes en 40%.</li>
        <li>Generación de reportes operativos con KPIs y análisis de SLAs; identificación de tendencias y propuesta de mejoras al equipo ITSM.</li>
        <li>Capacitación a usuarios finales en la plataforma ServiceNow y documentación de procedimientos de soporte.</li>
      </ul>
    </div>

    <!-- Itaipú Binacional - Analista TI -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-gray-400 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Analista de Soporte TI</p>
          <p class="text-sm text-gray-600 font-medium">Itaipú Binacional</p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Ene 2020 – Sep 2023</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Soporte técnico de hardware, software y redes para 500+ usuarios con uptime sostenido &gt;99.5%.</li>
        <li>Administración de Windows Server: Active Directory, GPOs, políticas de seguridad y servidor de impresión centralizado.</li>
        <li>Gestión de virtualización empresarial con Hyper-V y VMware; creación de imágenes con Sysprep y PXE.</li>
        <li>Administración de MECM: despliegue automatizado de sistemas operativos y aplicaciones corporativas.</li>
        <li>Gestión de inventario de activos TI y coordinación con proveedores para compras tecnológicas.</li>
      </ul>
    </div>

    <!-- Técnico de Redes -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-gray-300 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Técnico de Redes</p>
          <p class="text-sm text-gray-600 font-medium">Itaipú Binacional</p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Mar 2019 – Ene 2020</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Diagnóstico y resolución de problemas de conectividad a nivel físico y lógico: TCP/IP, VLANs, switches, routers y firewalls.</li>
        <li>Monitoreo de infraestructura crítica de red; mantenimiento preventivo para garantizar disponibilidad &gt;99%.</li>
        <li>Documentación de incidencias, procedimientos de resolución y registro técnico de cambios en la infraestructura.</li>
      </ul>
    </div>

  </div>
</section>

<!-- ENGLISH -->
<section data-lang="en" class="hidden py-12 px-6 max-w-4xl mx-auto">
  <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-8">Professional Experience</h2>

  <div class="relative pl-6 border-l-2 border-gray-200 flex flex-col gap-10">

    <!-- Parque Tecnológico Itaipú -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-blue-600 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Full-Stack Python Developer</p>
          <p class="text-sm text-blue-600 font-medium">Parque Tecnológico Itaipú</p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Feb 2025 – Present</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Development of specialized desktop applications in Python with PySide6/Qt Framework for electrical substation systems under the IEC 61850 standard.</li>
        <li>Implementation of decoupled architecture with SOLID principles and a service layer (AppService) for Frontend/Backend communication.</li>
        <li>Construction of interactive visual interfaces with real-time data validation for high-availability industrial environments.</li>
        <li>Development of features for IED (Intelligent Electronic Devices) configuration ensuring interoperability in substation ecosystems.</li>
        <li>Technical documentation of architecture decisions and quality processes; agile collaboration in a multidisciplinary team.</li>
      </ul>
    </div>

    <!-- Itaipú Binacional - Service Desk -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-gray-400 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Remote Support Analyst – Service Desk</p>
          <p class="text-sm text-gray-600 font-medium">Itaipú Binacional <span class="text-gray-400">(via Datapar / STI S.A.)</span></p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Sep 2023 – Feb 2025</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Intensive ServiceNow management: full lifecycle of incidents, problems, changes, and requests for 500+ enterprise users.</li>
        <li>Development of PowerShell scripts for Active Directory queries, reducing incident resolution time by 40%.</li>
        <li>Generation of operational reports with KPIs and SLA analysis; trend identification and process improvement proposals.</li>
        <li>End-user training on the ServiceNow platform and authoring of support procedure documentation.</li>
      </ul>
    </div>

    <!-- Itaipú Binacional - IT Support Analyst -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-gray-400 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">IT Support Analyst</p>
          <p class="text-sm text-gray-600 font-medium">Itaipú Binacional</p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Jan 2020 – Sep 2023</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Hardware, software, and network technical support for 500+ users with sustained uptime &gt;99.5%.</li>
        <li>Windows Server administration: Active Directory, GPOs, security policies, and centralized print server.</li>
        <li>Enterprise virtualization with Hyper-V and VMware; OS image creation with Sysprep and PXE.</li>
        <li>MECM administration: automated deployment of operating systems and corporate applications.</li>
        <li>IT asset inventory management and vendor coordination for technology procurement.</li>
      </ul>
    </div>

    <!-- Network Technician -->
    <div class="relative">
      <div class="absolute -left-[29px] top-1 w-3.5 h-3.5 rounded-full bg-gray-300 border-2 border-white"></div>
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-1 mb-2">
        <div>
          <p class="font-bold text-gray-900">Network Technician</p>
          <p class="text-sm text-gray-600 font-medium">Itaipú Binacional</p>
        </div>
        <span class="text-xs text-gray-400 whitespace-nowrap">Mar 2019 – Jan 2020</span>
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Diagnosis and resolution of connectivity issues at physical and logical layers: TCP/IP, VLANs, switches, routers, and firewalls.</li>
        <li>Critical network infrastructure monitoring; preventive maintenance to ensure availability &gt;99%.</li>
        <li>Incident documentation, resolution procedures, and technical change records for the infrastructure.</li>
      </ul>
    </div>

  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/portfolio/ExperienceList.astro
git commit -m "feat: add ExperienceList component (bilingual)"
```

---

## Task 5: ProjectsList component

**Files:**
- Create: `src/components/portfolio/ProjectsList.astro`

- [ ] **Step 1: Crear el componente**

```astro
---
// src/components/portfolio/ProjectsList.astro
// Proyectos propios con stack y descripción. Bilingüe.
---

<!-- ESPAÑOL -->
<section data-lang="es" class="py-12 px-6 max-w-4xl mx-auto">
  <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Proyectos Propios</h2>
  <p class="text-xs text-gray-400 mb-6">lucassim.com.py</p>

  <div class="flex flex-col gap-5">

    <!-- VareApp -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">VareApp</p>
          <p class="text-sm text-gray-500">SaaS de pedidos gastronómicos para restaurantes y food trucks</p>
        </div>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['Python', 'Flask', 'MongoDB', 'TailwindCSS', 'Cloudinary', 'Docker', 'WhatsApp API'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Sistema web multi-tenant con catálogo público, checkout e integración WhatsApp.</li>
        <li>Módulos: caja con IVA y factura electrónica (SIFEN Paraguay), inventario con alertas de stock, dashboard de métricas y roles admin/staff por tenant.</li>
        <li>Arquitectura desacoplada con Marshmallow para validación; gestión de categorías con drag & drop.</li>
      </ul>
    </div>

    <!-- Slotr -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">Slotr</p>
          <p class="text-sm text-gray-500">SaaS de agendamiento online multi-tenant</p>
        </div>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['Python', 'Flask', 'PostgreSQL', 'Telegram Bot API', 'Docker', 'Render', 'CI/CD'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Plataforma de turnos online para clínicas, peluquerías y canchas deportivas con múltiples negocios activos en producción.</li>
        <li>Reducción del 60% en tiempos de espera para los clientes finales.</li>
        <li>Calendarios por recurso/profesional, notificaciones Telegram, analytics dashboard y CI/CD automatizado en Render.</li>
      </ul>
    </div>

    <!-- MedicFile -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">MedicFile</p>
          <p class="text-sm text-gray-500">Ganador Hackathon Penguin Academy 2023</p>
        </div>
        <span class="px-2 py-0.5 bg-yellow-50 text-yellow-700 rounded text-xs font-medium whitespace-nowrap">🏆 Hackathon</span>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['Flask', 'SQLAlchemy', 'TailwindCSS', 'QR Code', 'Pillow'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>App web de registros médicos de emergencia con generación dinámica de código QR para acceso rápido a información crítica.</li>
        <li>Diseño mobile-first, APIs REST con validación completa.</li>
      </ul>
    </div>

    <!-- Herramientas -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">Herramientas de Infraestructura & APIs</p>
          <p class="text-sm text-gray-500">Utilidades internas y scripts de automatización</p>
        </div>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['PowerShell', 'Python', 'Flask', 'BeautifulSoup', 'SMTP', 'Active Directory'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Web Scraping API: API Flask para consultas de datos financieros con BeautifulSoup y cobertura de tests con Pytest.</li>
        <li>Mailer API: servicio de envío de emails con Flask y SMTP, validación de entradas y manejo de errores.</li>
        <li>AD Query Tool: herramienta CLI en PowerShell para consultas automatizadas en Active Directory.</li>
      </ul>
    </div>

  </div>
</section>

<!-- ENGLISH -->
<section data-lang="en" class="hidden py-12 px-6 max-w-4xl mx-auto">
  <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Own Projects</h2>
  <p class="text-xs text-gray-400 mb-6">lucassim.com.py</p>

  <div class="flex flex-col gap-5">

    <!-- VareApp -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">VareApp</p>
          <p class="text-sm text-gray-500">Gastronomic ordering SaaS for restaurants and food trucks</p>
        </div>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['Python', 'Flask', 'MongoDB', 'TailwindCSS', 'Cloudinary', 'Docker', 'WhatsApp API'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Multi-tenant web system with public catalog, checkout, and WhatsApp integration.</li>
        <li>Modules: POS with VAT and electronic invoicing (SIFEN Paraguay), inventory with stock alerts, metrics dashboard, and admin/staff roles per tenant.</li>
        <li>Decoupled architecture with Marshmallow for validation; drag & drop category management.</li>
      </ul>
    </div>

    <!-- Slotr -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">Slotr</p>
          <p class="text-sm text-gray-500">Multi-tenant online scheduling SaaS</p>
        </div>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['Python', 'Flask', 'PostgreSQL', 'Telegram Bot API', 'Docker', 'Render', 'CI/CD'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Online appointment platform for clinics, barber shops, and sports courts with multiple active businesses in production.</li>
        <li>60% reduction in customer wait times.</li>
        <li>Per-resource/professional calendars, Telegram notifications, analytics dashboard, and automated CI/CD on Render.</li>
      </ul>
    </div>

    <!-- MedicFile -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">MedicFile</p>
          <p class="text-sm text-gray-500">Winner — Penguin Academy Hackathon 2023</p>
        </div>
        <span class="px-2 py-0.5 bg-yellow-50 text-yellow-700 rounded text-xs font-medium whitespace-nowrap">🏆 Hackathon</span>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['Flask', 'SQLAlchemy', 'TailwindCSS', 'QR Code', 'Pillow'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Emergency medical record web app with dynamic QR code generation for quick access to critical information.</li>
        <li>Mobile-first design, REST APIs with full validation.</li>
      </ul>
    </div>

    <!-- Herramientas -->
    <div class="bg-white border border-gray-200 rounded-xl p-6">
      <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-2 mb-3">
        <div>
          <p class="font-bold text-gray-900 text-lg">Infrastructure Tools & APIs</p>
          <p class="text-sm text-gray-500">Internal utilities and automation scripts</p>
        </div>
      </div>
      <div class="flex flex-wrap gap-1.5 mb-4">
        {['PowerShell', 'Python', 'Flask', 'BeautifulSoup', 'SMTP', 'Active Directory'].map(t => (
          <span class="px-2 py-0.5 bg-blue-50 text-blue-700 rounded text-xs font-medium">{t}</span>
        ))}
      </div>
      <ul class="text-sm text-gray-600 flex flex-col gap-1.5 list-disc list-inside">
        <li>Web Scraping API: Flask API for financial data queries using BeautifulSoup with Pytest test coverage.</li>
        <li>Mailer API: email sending service with Flask and SMTP, input validation, and error handling.</li>
        <li>AD Query Tool: PowerShell CLI for automated Active Directory queries.</li>
      </ul>
    </div>

  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/portfolio/ProjectsList.astro
git commit -m "feat: add ProjectsList component (bilingual)"
```

---

## Task 6: EducationCerts component

**Files:**
- Create: `src/components/portfolio/EducationCerts.astro`

- [ ] **Step 1: Crear el componente**

```astro
---
// src/components/portfolio/EducationCerts.astro
// Educación y certificaciones en dos columnas. Bilingüe.
---

<!-- ESPAÑOL -->
<section data-lang="es" class="py-12 px-6 max-w-4xl mx-auto">
  <div class="grid sm:grid-cols-2 gap-8">

    <!-- Educación -->
    <div>
      <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Educación</h2>
      <div class="flex flex-col gap-4">
        <div>
          <p class="font-semibold text-gray-900 text-sm">Ingeniería de Sistemas con énfasis en TICs</p>
          <p class="text-xs text-gray-500">Facultad Politécnica — UNE</p>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-sm">Postgrado en Didáctica Universitaria</p>
          <p class="text-xs text-gray-500">Escuela de Posgrado — UNE</p>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-sm">Diplomado en Administración de Sistemas Linux</p>
          <p class="text-xs text-gray-500">UAA — Universidad Autónoma de Asunción</p>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-sm">Diplomado en Herramientas Forenses</p>
          <p class="text-xs text-gray-500">Corte Suprema de Justicia</p>
        </div>
      </div>
    </div>

    <!-- Certificaciones -->
    <div>
      <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Certificaciones</h2>
      <div class="flex flex-col gap-5">

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Cloud & Infraestructura</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['AWS Certified Cloud Practitioner', 'Amazon Web Services'],
              ['Microsoft Azure Fundamentals (AZ-900)', 'Microsoft'],
              ['Microsoft 365 Fundamentals (MS-900)', 'Microsoft'],
              ['Linux Essentials', 'Linux Professional Institute (LPI)'],
              ['RHCSA Rapid Track (RH199)', 'Red Hat'],
              ['CCNA: Introduction to Networks', 'Cisco'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Gestión de Servicios TI</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['ITIL 4 Foundation Certificate in ITSM', 'AXELOS'],
              ['Confluence Fundamentals', 'Atlassian'],
              ['Jira Fundamentals', 'Atlassian'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Desarrollo & Metodologías</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['Python Coding Bootcamp', 'Penguin Academy'],
              ['Scrum Foundation Professional', 'CertiProf'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Seguridad</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['ISO 27001 Internal Auditor Bootcamp', 'Hacker Mentor'],
              ['Cybersecurity Essentials', 'Cisco Networking Academy'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

      </div>
    </div>

  </div>
</section>

<!-- ENGLISH -->
<section data-lang="en" class="hidden py-12 px-6 max-w-4xl mx-auto">
  <div class="grid sm:grid-cols-2 gap-8">

    <!-- Education -->
    <div>
      <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Education</h2>
      <div class="flex flex-col gap-4">
        <div>
          <p class="font-semibold text-gray-900 text-sm">Systems Engineering with emphasis in ICTs</p>
          <p class="text-xs text-gray-500">Facultad Politécnica — UNE</p>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-sm">Postgraduate in University Didactics</p>
          <p class="text-xs text-gray-500">Escuela de Posgrado — UNE</p>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-sm">Diploma in Linux Systems Administration</p>
          <p class="text-xs text-gray-500">UAA — Universidad Autónoma de Asunción</p>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-sm">Diploma in Forensic Tools</p>
          <p class="text-xs text-gray-500">Corte Suprema de Justicia</p>
        </div>
      </div>
    </div>

    <!-- Certifications -->
    <div>
      <h2 class="text-xs text-gray-400 uppercase tracking-widest mb-6">Certifications</h2>
      <div class="flex flex-col gap-5">

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Cloud & Infrastructure</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['AWS Certified Cloud Practitioner', 'Amazon Web Services'],
              ['Microsoft Azure Fundamentals (AZ-900)', 'Microsoft'],
              ['Microsoft 365 Fundamentals (MS-900)', 'Microsoft'],
              ['Linux Essentials', 'Linux Professional Institute (LPI)'],
              ['RHCSA Rapid Track (RH199)', 'Red Hat'],
              ['CCNA: Introduction to Networks', 'Cisco'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">IT Service Management</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['ITIL 4 Foundation Certificate in ITSM', 'AXELOS'],
              ['Confluence Fundamentals', 'Atlassian'],
              ['Jira Fundamentals', 'Atlassian'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Development & Methodologies</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['Python Coding Bootcamp', 'Penguin Academy'],
              ['Scrum Foundation Professional', 'CertiProf'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-600 mb-2">Security</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['ISO 27001 Internal Auditor Bootcamp', 'Hacker Mentor'],
              ['Cybersecurity Essentials', 'Cisco Networking Academy'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-gray-600">
                <span class="font-medium text-gray-800">{name}</span>
                <span class="text-gray-400"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

      </div>
    </div>

  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/portfolio/EducationCerts.astro
git commit -m "feat: add EducationCerts component (bilingual)"
```

---

## Task 7: Main portfolio page + toggle script + build verification

**Files:**
- Create: `src/pages/portfolio.astro`

- [ ] **Step 1: Crear la página principal**

```astro
---
// src/pages/portfolio.astro
import BaseLayout from '../layouts/BaseLayout.astro';
import PortfolioNavbar from '../components/portfolio/PortfolioNavbar.astro';
import PortfolioHero from '../components/portfolio/PortfolioHero.astro';
import SkillsGrid from '../components/portfolio/SkillsGrid.astro';
import ExperienceList from '../components/portfolio/ExperienceList.astro';
import ProjectsList from '../components/portfolio/ProjectsList.astro';
import EducationCerts from '../components/portfolio/EducationCerts.astro';
---

<BaseLayout
  title="Lucas S. Paniagua — Portfolio"
  description="Portfolio profesional de Lucas S. Paniagua: Full-Stack Developer, System Administrator y Support Engineer con 5+ años de experiencia."
>
  <!-- Wrapper claro que cubre el bg-base del body definido en BaseLayout -->
  <div class="bg-gray-50 text-gray-900 min-h-screen font-sans">
    <PortfolioNavbar />

    <main>
      <PortfolioHero />

      <!-- Divisor -->
      <div class="max-w-4xl mx-auto px-6">
        <hr class="border-gray-200" />
      </div>

      <SkillsGrid />

      <div class="max-w-4xl mx-auto px-6">
        <hr class="border-gray-200" />
      </div>

      <ExperienceList />

      <div class="max-w-4xl mx-auto px-6">
        <hr class="border-gray-200" />
      </div>

      <ProjectsList />

      <div class="max-w-4xl mx-auto px-6">
        <hr class="border-gray-200" />
      </div>

      <EducationCerts />
    </main>

    <!-- Footer light inline -->
    <footer class="border-t border-gray-200 mt-8">
      <div class="max-w-4xl mx-auto px-6 py-6 flex flex-col sm:flex-row items-center justify-between gap-2">
        <span class="text-sm font-bold text-gray-900">lucassim</span>
        <span class="text-xs text-gray-400">© {new Date().getFullYear()} Lucas S. Paniagua · lucassim.com.py</span>
        <div class="flex gap-4">
          <a href="https://github.com/paniagua788" class="text-xs text-gray-500 hover:text-gray-900 transition-colors">GitHub</a>
          <a href="https://linkedin.com/in/paniagua788" class="text-xs text-gray-500 hover:text-gray-900 transition-colors">LinkedIn</a>
        </div>
      </div>
    </footer>
  </div>

  <!-- Toggle script: alterna data-lang="es" / data-lang="en" -->
  <script>
    (function () {
      var btns = document.querySelectorAll('[data-lang-btn]');
      var sections = document.querySelectorAll('[data-lang]');

      function setLang(lang) {
        sections.forEach(function (el) {
          if (el instanceof HTMLElement) {
            el.classList.toggle('hidden', el.dataset.lang !== lang);
          }
        });
        btns.forEach(function (btn) {
          if (btn instanceof HTMLElement) {
            var active = btn.dataset.target === lang;
            btn.classList.toggle('bg-gray-900', active);
            btn.classList.toggle('text-white', active);
            btn.classList.toggle('text-gray-500', !active);
          }
        });
      }

      btns.forEach(function (btn) {
        btn.addEventListener('click', function () {
          if (btn instanceof HTMLElement && btn.dataset.target) {
            setLang(btn.dataset.target);
          }
        });
      });
    })();
  </script>
</BaseLayout>
```

- [ ] **Step 2: Correr build de producción**

```bash
npm run build
```

Esperado: compilación exitosa sin errores ni warnings críticos. La ruta `/portfolio` debe aparecer en el output de Astro.

- [ ] **Step 3: Verificar en dev server** (opcional pero recomendado)

```bash
npm run dev
```

Navegar a `http://localhost:4321/portfolio` y verificar:
- Fondo blanco/gris claro visible
- Navbar fijo con botones ES/EN y "← Volver"
- Toggle ES→EN cambia todos los textos correctamente
- Toggle EN→ES regresa al español sin recargar página
- Todas las secciones visibles: Hero, Skills, Experiencia, Proyectos, Educación+Certs

- [ ] **Step 4: Commit final**

```bash
git add src/pages/portfolio.astro
git commit -m "feat: add /portfolio page with bilingual toggle (ES/EN)"
```

---

## Self-Review

**Spec coverage:**
- ✅ Ruta `/portfolio` — `src/pages/portfolio.astro`
- ✅ Tema claro (bg-gray-50, bg-white) — sin modificar global.css
- ✅ Toggle ES/EN con script vanilla — Task 7 step 1
- ✅ Secciones en orden: Hero → Skills → Experiencia → Proyectos → Edu+Certs
- ✅ PortfolioNavbar con "← Volver" — Task 1
- ✅ Todo el contenido del CV — Tasks 2-6
- ✅ Bilingüe con data-lang pattern — en todos los componentes
- ✅ Sin modificar global.css ni tailwind.config — confirmado
- ✅ Verificación con npm run build — Task 7 step 2

**Sin placeholders:** revisado — todos los pasos contienen código completo.

**Consistencia de tipos:** el atributo `data-lang` y `data-lang-btn` se usan consistentemente en todos los componentes y en el script de Task 7. El script busca `[data-lang-btn]` (definido en PortfolioNavbar, Task 1) y `[data-lang]` (definido en todos los demás componentes, Tasks 2-6).
