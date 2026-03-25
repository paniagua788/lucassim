# lucassim.com.py

Sitio web personal de [lucassim](https://lucassim.com.py) — Ingeniero de Sistemas paraguayo, desarrollador independiente de soluciones SaaS.

🌐 **[lucassim.com.py](https://lucassim.com.py)**

---

## Páginas

| Ruta | Descripción |
|---|---|
| `/` | Home — presentación personal y productos |
| `/vareapp` | Landing page de [VareApp](https://lucassim.com.py/vareapp) |
| `/slotr` | Landing page de [Slotr](https://lucassim.com.py/slotr) |

## Stack

- [Astro 6](https://astro.build) — framework de sitios estáticos
- [Tailwind CSS 4](https://tailwindcss.com) — estilos
- [Cloudflare Pages](https://pages.cloudflare.com) — deploy y hosting

## Desarrollo local

```bash
npm install
npm run dev
```

Abrí `http://localhost:4321` en el navegador.

## Deploy

El deploy es automático: cada push a `main` redeploya el sitio en Cloudflare Pages.

```bash
npm run build   # build de producción → dist/
```
