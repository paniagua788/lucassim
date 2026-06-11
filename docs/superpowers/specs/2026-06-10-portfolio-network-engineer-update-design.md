# Design: Portfolio Network Engineer Profile Update

## Goal
Strengthen the portfolio's emphasis on the Network Engineer profile by updating roles, expanding relevant experience descriptions, and adding key certifications.

## Files to Modify

1. `src/pages/portfolio.astro`
2. `src/components/portfolio/PortfolioHero.astro`
3. `src/components/portfolio/ExperienceList.astro`
4. `src/components/portfolio/EducationCerts.astro`

## Changes

### 1. `src/pages/portfolio.astro` (Meta Description)
- Update the `<meta name="description">` tag to include "Network Engineer" in the list of roles.

### 2. `src/components/portfolio/PortfolioHero.astro`
- **Roles badges (ES + EN):** Add a new `Network Engineer` badge alongside the existing `Full-Stack Developer`, `System Administrator`, and `Support Engineer` badges.
- **Bio text (ES):** Update the bio to mention network infrastructure design, diagnosis, and resolution as part of the expertise.
- **Bio text (EN):** Translate the updated bio content.

### 3. `src/components/portfolio/ExperienceList.astro`
- **"Técnico de Redes" / "Network Technician" (ES + EN):** Expand bullet points to highlight network design (topologies, VLAN planning, subnetting), advanced troubleshooting (routing, switching, firewalls), and technical infrastructure documentation.
- **"Analista de Soporte TI" / "IT Support Analyst" (ES + EN):** Add a bullet point emphasizing on-site network diagnosis and resolution (cabling, switches, access points) and collaboration with the network team.
- **"Analista de Soporte Remoto" / "Remote Support Analyst" (ES + EN):** Add a bullet point emphasizing remote connectivity troubleshooting, VPN diagnostics, and network performance analysis for distributed users.

### 4. `src/components/portfolio/EducationCerts.astro`
- **Cloud & Infraestructura / Cloud & Infrastructure (ES + EN):**
  - Add: `Tecnólogo de Redes` — SNPP
  - Add: `Cloud Computing` — SNPP
- **Seguridad / Security (ES + EN):**
  - Add: `Introduction to Cybersecurity` — Cisco Networking Academy
- **New Category — Redes e IoT / Networking & IoT (ES + EN):**
  - Add: `Introduction to IoT` — Cisco
- **New Category — Idiomas / Languages (ES + EN):**
  - Add: `EF SET English Certificate C1 Advanced` — EF SET

## Constraints
- Keep changes minimal and focused; do not refactor unrelated components.
- Maintain existing styling, bilingual structure (`data-lang="es"` / `data-lang="en"`), and formatting patterns.
- No new dependencies or assets required.
