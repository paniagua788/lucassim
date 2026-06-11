# Portfolio Network Engineer Profile Update - Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Strengthen the portfolio's emphasis on the Network Engineer profile by adding the role badge, extending experience descriptions, and adding key certifications.

**Architecture:** Static Astro site with bilingual content (ES/EN). Changes are text edits to existing components. No new dependencies.

**Tech Stack:** Astro 6, Tailwind CSS 4, TypeScript strict.

---

## File Map

| File | Changes |
|------|---------|
| `src/pages/portfolio.astro` | Meta description update |
| `src/components/portfolio/PortfolioHero.astro` | Add Network Engineer badge (ES+EN), update bio |
| `src/components/portfolio/ExperienceList.astro` | Extend Técnico de Redes bullets, add network bullets to Analista de Soporte TI and Analista de Soporte Remoto |
| `src/components/portfolio/EducationCerts.astro` | Add 5 new certifications in new and existing categories |

---

## Tasks

### Task 1: Update Meta Description

**Files:**
- Modify: `src/pages/portfolio.astro:14`

- [ ] **Step 1: Update meta description**

Find line 14:
```astro
description="Portfolio profesional de Lucas S. Paniagua: Full-Stack Developer, System Administrator y Support Engineer con 5+ años de experiencia."
```

Replace with:
```astro
description="Portfolio profesional de Lucas S. Paniagua: Network Engineer, Full-Stack Developer, System Administrator y Support Engineer con 5+ años de experiencia."
```

---

### Task 2: Add Network Engineer Badge and Update Bio (ES + EN)

**Files:**
- Modify: `src/components/portfolio/PortfolioHero.astro:14-18` (ES badges)
- Modify: `src/components/portfolio/PortfolioHero.astro:20-26` (ES bio)
- Modify: `src/components/portfolio/PortfolioHero.astro:78-82` (EN badges)
- Modify: `src/components/portfolio/PortfolioHero.astro:84-90` (EN bio)

- [ ] **Step 1: Add Network Engineer badge (ES)**

Find lines 14-18:
```astro
<div class="flex flex-wrap gap-2 mb-6">
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Full-Stack Developer</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">System Administrator</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Support Engineer</span>
</div>
```

Replace with:
```astro
<div class="flex flex-wrap gap-2 mb-6">
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Network Engineer</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Full-Stack Developer</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">System Administrator</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Support Engineer</span>
</div>
```

- [ ] **Step 2: Update Spanish bio**

Find lines 20-26:
```astro
<p class="text-muted max-w-2xl leading-relaxed mb-8">
  Ingeniero de Sistemas con 5+ años de experiencia en desarrollo de software, administración de
  infraestructura y gestión de servicios TI. Construyo aplicaciones Full-Stack en Python y
  JavaScript con SaaS propios en producción; opero entornos empresariales de alta demanda
  (~2.500 usuarios, uptime &gt;99.5%) con expertise en ITSM/ServiceNow, troubleshooting sistemático
  y gestión de activos. Certificado en ITIL 4, AWS Cloud Practitioner, Scrum, LPI e ISO 27001.
</p>
```

Replace with:
```astro
<p class="text-muted max-w-2xl leading-relaxed mb-8">
  Ingeniero de Sistemas con 5+ años de experiencia en diseño, diagnóstico y resolución de
  infraestructura de red, desarrollo de software, administración de sistemas y gestión de
  servicios TI. Construyo aplicaciones Full-Stack en Python y JavaScript con SaaS propios en
  producción; opero entornos empresariales de alta demanda (~2.500 usuarios, uptime &gt;99.5%)
  con expertise en networking, ITSM/ServiceNow, troubleshooting sistemático y gestión de activos.
  Certificado en ITIL 4, AWS Cloud Practitioner, Scrum, LPI, CCNA e ISO 27001.
</p>
```

- [ ] **Step 3: Add Network Engineer badge (EN)**

Find lines 78-82:
```astro
<div class="flex flex-wrap gap-2 mb-6">
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Full-Stack Developer</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">System Administrator</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Support Engineer</span>
</div>
```

Replace with:
```astro
<div class="flex flex-wrap gap-2 mb-6">
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Network Engineer</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Full-Stack Developer</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">System Administrator</span>
  <span class="px-3 py-1 bg-surface text-muted rounded-full text-xs font-semibold">Support Engineer</span>
</div>
```

- [ ] **Step 4: Update English bio**

Find lines 84-90:
```astro
<p class="text-muted max-w-2xl leading-relaxed mb-8">
  Systems Engineer with 5+ years of experience across software development, infrastructure
  administration, and IT service management. I build Full-Stack applications in Python and
  JavaScript with own SaaS products in production, and operate high-demand enterprise environments
  (~2,500 users, uptime &gt;99.5%) with expertise in ITSM/ServiceNow, systematic troubleshooting,
  and asset management. ITIL 4, AWS Cloud Practitioner, Scrum, LPI, and ISO 27001 certified.
</p>
```

Replace with:
```astro
<p class="text-muted max-w-2xl leading-relaxed mb-8">
  Systems Engineer with 5+ years of experience in network infrastructure design, diagnosis,
  and resolution, software development, systems administration, and IT service management.
  I build Full-Stack applications in Python and JavaScript with own SaaS products in production,
  and operate high-demand enterprise environments (~2,500 users, uptime &gt;99.5%) with expertise
  in networking, ITSM/ServiceNow, systematic troubleshooting, and asset management. ITIL 4,
  AWS Cloud Practitioner, Scrum, LPI, CCNA, and ISO 27001 certified.
</p>
```

---

### Task 3: Extend Técnico de Redes Experience (ES + EN)

**Files:**
- Modify: `src/components/portfolio/ExperienceList.astro:84-88` (ES bullets)
- Modify: `src/components/portfolio/ExperienceList.astro:172-176` (EN bullets)

- [ ] **Step 1: Extend Spanish Técnico de Redes bullets**

Find lines 84-88:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Diagnóstico y resolución de problemas de conectividad a nivel físico y lógico: TCP/IP, VLANs, switches, routers y firewalls.</li>
  <li>Monitoreo de infraestructura crítica de red; mantenimiento preventivo para garantizar disponibilidad &gt;99%.</li>
  <li>Documentación de incidencias, procedimientos de resolución y registro técnico de cambios en la infraestructura.</li>
</ul>
```

Replace with:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Diseño y planificación de topologías de red, segmentación mediante VLANs y plan de direccionamiento IP (subnetting) para optimizar el tráfico y la seguridad de la infraestructura.</li>
  <li>Diagnóstico y resolución avanzada de problemas de conectividad a nivel físico y lógico: TCP/IP, VLANs, STP, routing estático y dinámico (OSPF), switches, routers y firewalls.</li>
  <li>Configuración y mantenimiento de dispositivos de red (switches gestionables, routers, firewalls) para garantizar la disponibilidad y seguridad de la red corporativa &gt;99%.</li>
  <li>Monitoreo proactivo de infraestructura crítica de red; implementación de mantenimiento preventivo y planes de mejora continua.</li>
  <li>Documentación técnica de incidencias, procedimientos de resolución, diagramas de red y registros de cambios en la infraestructura.</li>
</ul>
```

- [ ] **Step 2: Extend English Network Technician bullets**

Find lines 172-176:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Diagnosis and resolution of connectivity issues at physical and logical layers: TCP/IP, VLANs, switches, routers, and firewalls.</li>
  <li>Critical network infrastructure monitoring; preventive maintenance to ensure availability &gt;99%.</li>
  <li>Incident documentation, resolution procedures, and technical change records for the infrastructure.</li>
</ul>
```

Replace with:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Network topology design and planning, VLAN segmentation, and IP addressing planning (subnetting) to optimize traffic flow and infrastructure security.</li>
  <li>Advanced diagnosis and resolution of connectivity issues at physical and logical layers: TCP/IP, VLANs, STP, static and dynamic routing (OSPF), switches, routers, and firewalls.</li>
  <li>Configuration and maintenance of network devices (managed switches, routers, firewalls) to ensure corporate network availability and security &gt;99%.</li>
  <li>Proactive critical network infrastructure monitoring; preventive maintenance implementation and continuous improvement plans.</li>
  <li>Technical incident documentation, resolution procedures, network diagrams, and infrastructure change records.</li>
</ul>
```

---

### Task 4: Add Network Bullet to Analista de Soporte TI (ES + EN)

**Files:**
- Modify: `src/components/portfolio/ExperienceList.astro:62-71` (ES bullets)
- Modify: `src/components/portfolio/ExperienceList.astro:150-159` (EN bullets)

- [ ] **Step 1: Add network bullet to Spanish Analista de Soporte TI**

Find lines 62-71:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Soporte técnico de hardware, software y redes para división de microinformática (500+ usuarios) con uptime sostenido &gt;99.5%.</li>
  <li>Administración de Windows Server: Active Directory, GPOs, políticas de seguridad, servidor de impresión centralizado (Equitrac) y servicios de dominio.</li>
  <li>Gestión de virtualización empresarial con Hyper-V y VMware (100+ VMs); creación y distribución de imágenes de sistema con Sysprep y PXE.</li>
  <li>Administración de Microsoft Endpoint Configuration Manager (MECM): despliegue automatizado de sistemas operativos y aplicaciones corporativas.</li>
  <li>Gestión de inventario de activos TI (hardware, software y licencias); coordinación con proveedores para compras tecnológicas, cotizaciones y seguimiento presupuestario.</li>
  <li>Administración de sistemas de almacenamiento y backup empresarial; implementación de políticas de respaldo y recuperación de datos críticos.</li>
  <li>Prospección tecnológica, elaboración de especificaciones técnicas y pareceres técnicos para procesos de adquisición de equipos informáticos (notebooks, AIOs, proyectores, entre otros); participación en migraciones de servicios legacy a arquitecturas virtualizadas.</li>
  <li>Colaboración en auditorías internas de infraestructura y actualización de documentación técnica.</li>
</ul>
```

Replace with:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Soporte técnico de hardware, software y redes para división de microinformática (500+ usuarios) con uptime sostenido &gt;99.5%.</li>
  <li>Diagnóstico y resolución de problemas de conectividad de red en sitio: cableado estructurado, switches, puntos de acceso y enlaces de comunicación; colaboración con el equipo de redes para escalación y seguimiento de incidencias.</li>
  <li>Administración de Windows Server: Active Directory, GPOs, políticas de seguridad, servidor de impresión centralizado (Equitrac) y servicios de dominio.</li>
  <li>Gestión de virtualización empresarial con Hyper-V y VMware (100+ VMs); creación y distribución de imágenes de sistema con Sysprep y PXE.</li>
  <li>Administración de Microsoft Endpoint Configuration Manager (MECM): despliegue automatizado de sistemas operativos y aplicaciones corporativas.</li>
  <li>Gestión de inventario de activos TI (hardware, software y licencias); coordinación con proveedores para compras tecnológicas, cotizaciones y seguimiento presupuestario.</li>
  <li>Administración de sistemas de almacenamiento y backup empresarial; implementación de políticas de respaldo y recuperación de datos críticos.</li>
  <li>Prospección tecnológica, elaboración de especificaciones técnicas y pareceres técnicos para procesos de adquisición de equipos informáticos (notebooks, AIOs, proyectores, entre otros); participación en migraciones de servicios legacy a arquitecturas virtualizadas.</li>
  <li>Colaboración en auditorías internas de infraestructura y actualización de documentación técnica.</li>
</ul>
```

- [ ] **Step 2: Add network bullet to English IT Support Analyst**

Find lines 150-159:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Hardware, software, and network technical support for the microcomputing division (500+ users) with sustained uptime &gt;99.5%.</li>
  <li>Windows Server administration: Active Directory, GPOs, security policies, centralized print server (Equitrac), and domain services.</li>
  <li>Enterprise virtualization management with Hyper-V and VMware (100+ VMs); OS image creation and distribution with Sysprep and PXE.</li>
  <li>Microsoft Endpoint Configuration Manager (MECM) administration: automated deployment of operating systems and corporate applications.</li>
  <li>IT asset inventory management (hardware, software, and licenses); vendor coordination for technology procurement, quotes, and budget tracking.</li>
  <li>Enterprise storage and backup systems administration; implementation of backup policies and critical data recovery.</li>
  <li>Technology prospecting, technical specification drafting, and technical assessments for IT equipment acquisition processes (notebooks, AIOs, projectors, among others); participation in legacy service migration to virtualized architectures.</li>
  <li>Collaboration in internal infrastructure audits and technical documentation updates.</li>
</ul>
```

Replace with:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Hardware, software, and network technical support for the microcomputing division (500+ users) with sustained uptime &gt;99.5%.</li>
  <li>On-site network connectivity diagnosis and resolution: structured cabling, switches, access points, and communication links; collaboration with the network team for escalation and incident follow-up.</li>
  <li>Windows Server administration: Active Directory, GPOs, security policies, centralized print server (Equitrac), and domain services.</li>
  <li>Enterprise virtualization management with Hyper-V and VMware (100+ VMs); OS image creation and distribution with Sysprep and PXE.</li>
  <li>Microsoft Endpoint Configuration Manager (MECM) administration: automated deployment of operating systems and corporate applications.</li>
  <li>IT asset inventory management (hardware, software, and licenses); vendor coordination for technology procurement, quotes, and budget tracking.</li>
  <li>Enterprise storage and backup systems administration; implementation of backup policies and critical data recovery.</li>
  <li>Technology prospecting, technical specification drafting, and technical assessments for IT equipment acquisition processes (notebooks, AIOs, projectors, among others); participation in legacy service migration to virtualized architectures.</li>
  <li>Collaboration in internal infrastructure audits and technical documentation updates.</li>
</ul>
```

---

### Task 5: Add Network Bullet to Analista de Soporte Remoto (ES + EN)

**Files:**
- Modify: `src/components/portfolio/ExperienceList.astro:41-49` (ES bullets)
- Modify: `src/components/portfolio/ExperienceList.astro:129-137` (EN bullets)

- [ ] **Step 1: Add network bullet to Spanish Analista de Soporte Remoto**

Find lines 41-49:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Gestión intensiva de ServiceNow como usuario avanzado: ciclo completo de incidentes, problemas, cambios y solicitudes para 500+ usuarios empresariales.</li>
  <li>Desarrollo de scripts PowerShell para consultas automatizadas en Active Directory, reduciendo tiempos de resolución en un 40%.</li>
  <li>Generación de reportes operativos con KPIs y análisis de SLAs; identificación de tendencias y propuesta de mejoras al equipo de administración ITSM.</li>
  <li>Colaboración estrecha con el equipo de desarrollo ITSM: levantamiento de requerimientos funcionales, UAT de nuevas funcionalidades y validación de cambios antes de producción.</li>
  <li>Resolución del 99%+ de tickets sin necesidad de escalación a Tier 2/3 mediante troubleshooting sistemático.</li>
  <li>Capacitación a usuarios finales en la plataforma ServiceNow; documentación de procedimientos de soporte y guías de troubleshooting.</li>
  <li>Monitoreo proactivo de sistemas para detección temprana de incidentes antes de impacto a usuarios.</li>
</ul>
```

Replace with:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Gestión intensiva de ServiceNow como usuario avanzado: ciclo completo de incidentes, problemas, cambios y solicitudes para 500+ usuarios empresariales.</li>
  <li>Desarrollo de scripts PowerShell para consultas automatizadas en Active Directory, reduciendo tiempos de resolución en un 40%.</li>
  <li>Diagnóstico y resolución de problemas de conectividad remota y VPN para usuarios distribuidos; análisis de rendimiento de red y troubleshooting de enlaces de comunicación.</li>
  <li>Generación de reportes operativos con KPIs y análisis de SLAs; identificación de tendencias y propuesta de mejoras al equipo de administración ITSM.</li>
  <li>Colaboración estrecha con el equipo de desarrollo ITSM: levantamiento de requerimientos funcionales, UAT de nuevas funcionalidades y validación de cambios antes de producción.</li>
  <li>Resolución del 99%+ de tickets sin necesidad de escalación a Tier 2/3 mediante troubleshooting sistemático.</li>
  <li>Capacitación a usuarios finales en la plataforma ServiceNow; documentación de procedimientos de soporte y guías de troubleshooting.</li>
  <li>Monitoreo proactivo de sistemas para detección temprana de incidentes antes de impacto a usuarios.</li>
</ul>
```

- [ ] **Step 2: Add network bullet to English Remote Support Analyst**

Find lines 129-137:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Intensive ServiceNow management as an advanced user: full lifecycle of incidents, problems, changes, and requests for 500+ enterprise users.</li>
  <li>Development of PowerShell scripts for automated Active Directory queries, reducing resolution times by 40%.</li>
  <li>Generation of operational reports with KPIs and SLA analysis; trend identification and process improvement proposals to the ITSM administration team.</li>
  <li>Close collaboration with the ITSM development team: functional requirements gathering, UAT of new features, and change validation before production.</li>
  <li>Resolution of 99%+ of tickets without Tier 2/3 escalation through systematic troubleshooting.</li>
  <li>End-user training on the ServiceNow platform; authoring of support procedure documentation and troubleshooting guides.</li>
  <li>Proactive system monitoring for early incident detection before user impact.</li>
</ul>
```

Replace with:
```astro
<ul class="text-sm text-muted flex flex-col gap-1.5 list-disc list-inside">
  <li>Intensive ServiceNow management as an advanced user: full lifecycle of incidents, problems, changes, and requests for 500+ enterprise users.</li>
  <li>Development of PowerShell scripts for automated Active Directory queries, reducing resolution times by 40%.</li>
  <li>Remote connectivity and VPN troubleshooting for distributed users; network performance analysis and communication link troubleshooting.</li>
  <li>Generation of operational reports with KPIs and SLA analysis; trend identification and process improvement proposals to the ITSM administration team.</li>
  <li>Close collaboration with the ITSM development team: functional requirements gathering, UAT of new features, and change validation before production.</li>
  <li>Resolution of 99%+ of tickets without Tier 2/3 escalation through systematic troubleshooting.</li>
  <li>End-user training on the ServiceNow platform; authoring of support procedure documentation and troubleshooting guides.</li>
  <li>Proactive system monitoring for early incident detection before user impact.</li>
</ul>
```

---

### Task 6: Add New Certifications to EducationCerts.astro

**Files:**
- Modify: `src/components/portfolio/EducationCerts.astro:36-55` (ES Cloud & Infraestructura)
- Modify: `src/components/portfolio/EducationCerts.astro:88-101` (ES Security + new categories)
- Modify: `src/components/portfolio/EducationCerts.astro:139-158` (EN Cloud & Infrastructure)
- Modify: `src/components/portfolio/EducationCerts.astro:191-206` (EN Security + new categories)

- [ ] **Step 1: Add Tecnólogo de Redes and Cloud Computing to Spanish Cloud & Infraestructura**

Find lines 41-53:
```astro
{[
  ['AWS Certified Cloud Practitioner', 'Amazon Web Services'],
  ['Microsoft Azure Fundamentals (AZ-900)', 'Microsoft'],
  ['Microsoft 365 Fundamentals (MS-900)', 'Microsoft'],
  ['Linux Essentials', 'Linux Professional Institute (LPI)'],
  ['RHCSA Rapid Track (RH199)', 'Red Hat'],
  ['CCNA: Introduction to Networks', 'Cisco'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

Replace with:
```astro
{[
  ['AWS Certified Cloud Practitioner', 'Amazon Web Services'],
  ['Microsoft Azure Fundamentals (AZ-900)', 'Microsoft'],
  ['Microsoft 365 Fundamentals (MS-900)', 'Microsoft'],
  ['Linux Essentials', 'Linux Professional Institute (LPI)'],
  ['RHCSA Rapid Track (RH199)', 'Red Hat'],
  ['CCNA: Introduction to Networks', 'Cisco'],
  ['Tecnólogo de Redes', 'SNPP'],
  ['Cloud Computing', 'SNPP'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

- [ ] **Step 2: Add Introduction to Cybersecurity to Spanish Security section**

Find lines 91-99:
```astro
{[
  ['ISO 27001 Internal Auditor Bootcamp', 'Hacker Mentor'],
  ['Cybersecurity Essentials', 'Cisco Networking Academy'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

Replace with:
```astro
{[
  ['ISO 27001 Internal Auditor Bootcamp', 'Hacker Mentor'],
  ['Cybersecurity Essentials', 'Cisco Networking Academy'],
  ['Introduction to Cybersecurity', 'Cisco Networking Academy'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

- [ ] **Step 3: Add new "Redes e IoT" category after Security section (Spanish)**

Find lines 101-103 (before `</div>` closing Security div):
```astro
          </ul>
        </div>

        </div>
```

Replace with:
```astro
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-400 mb-2">Redes e IoT</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['Introduction to IoT', 'Cisco Networking Academy'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-muted">
                <span class="font-medium text-white">{name}</span>
                <span class="text-subtle"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-400 mb-2">Idiomas</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['EF SET English Certificate C1 Advanced (64/100)', 'EF SET'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-muted">
                <span class="font-medium text-white">{name}</span>
                <span class="text-subtle"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        </div>
```

- [ ] **Step 4: Add certifications to English Cloud & Infrastructure**

Find lines 144-156:
```astro
{[
  ['AWS Certified Cloud Practitioner', 'Amazon Web Services'],
  ['Microsoft Azure Fundamentals (AZ-900)', 'Microsoft'],
  ['Microsoft 365 Fundamentals (MS-900)', 'Microsoft'],
  ['Linux Essentials', 'Linux Professional Institute (LPI)'],
  ['RHCSA Rapid Track (RH199)', 'Red Hat'],
  ['CCNA: Introduction to Networks', 'Cisco'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

Replace with:
```astro
{[
  ['AWS Certified Cloud Practitioner', 'Amazon Web Services'],
  ['Microsoft Azure Fundamentals (AZ-900)', 'Microsoft'],
  ['Microsoft 365 Fundamentals (MS-900)', 'Microsoft'],
  ['Linux Essentials', 'Linux Professional Institute (LPI)'],
  ['RHCSA Rapid Track (RH199)', 'Red Hat'],
  ['CCNA: Introduction to Networks', 'Cisco'],
  ['Tecnólogo de Redes', 'SNPP'],
  ['Cloud Computing', 'SNPP'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

- [ ] **Step 5: Add Introduction to Cybersecurity to English Security section**

Find lines 194-202:
```astro
{[
  ['ISO 27001 Internal Auditor Bootcamp', 'Hacker Mentor'],
  ['Cybersecurity Essentials', 'Cisco Networking Academy'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

Replace with:
```astro
{[
  ['ISO 27001 Internal Auditor Bootcamp', 'Hacker Mentor'],
  ['Cybersecurity Essentials', 'Cisco Networking Academy'],
  ['Introduction to Cybersecurity', 'Cisco Networking Academy'],
].map(([name, issuer]) => (
  <li class="text-xs text-muted">
    <span class="font-medium text-white">{name}</span>
    <span class="text-subtle"> — {issuer}</span>
  </li>
))}
```

- [ ] **Step 6: Add new "Networking & IoT" and "Languages" categories (English)**

Find lines 203-205:
```astro
          </ul>
        </div>

        </div>
```

Replace with:
```astro
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-400 mb-2">Networking & IoT</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['Introduction to IoT', 'Cisco Networking Academy'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-muted">
                <span class="font-medium text-white">{name}</span>
                <span class="text-subtle"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        <div>
          <p class="text-xs font-semibold text-blue-400 mb-2">Languages</p>
          <ul class="flex flex-col gap-1.5">
            {[
              ['EF SET English Certificate C1 Advanced (64/100)', 'EF SET'],
            ].map(([name, issuer]) => (
              <li class="text-xs text-muted">
                <span class="font-medium text-white">{name}</span>
                <span class="text-subtle"> — {issuer}</span>
              </li>
            ))}
          </ul>
        </div>

        </div>
```

---

### Task 7: Verification

**Files:**
- Modify: None

- [ ] **Step 1: Run Astro type check**

Run: `npx astro check`
Expected: No TypeScript errors

- [ ] **Step 2: Run build to verify**

Run: `npm run build`
Expected: Successful build with no errors

- [ ] **Step 3: Test locally (optional)**

Run: `npm run dev` to visually verify changes at http://localhost:4321/portfolio

---

## Spec Coverage Check

| Spec Requirement | Task(s) |
|------------------|---------|
| Add Network Engineer badge | Task 2 |
| Update bio (ES+EN) with networking emphasis | Task 2 |
| Update meta description | Task 1 |
| Extend Técnico de Redes bullets | Task 3 |
| Add network bullet to Analista de Soporte TI | Task 4 |
| Add network bullet to Analista de Soporte Remoto | Task 5 |
| Add Tecnólogo de Redes and Cloud Computing | Task 6 |
| Add Introduction to Cybersecurity | Task 6 |
| Add Introduction to IoT (new category) | Task 6 |
| Add EF SET English C1 Advanced (new category) | Task 6 |

All spec requirements covered.

---

## Placeholder Scan

No placeholders found. All steps contain complete code and exact file paths.
