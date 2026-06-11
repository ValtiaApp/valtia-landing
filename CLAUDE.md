# CLAUDE.md

Landing page de Valtia ("valor y análisis", consultoría de investigación de mercado). Sitio estático con Astro + Tailwind CSS, diseñado originalmente en Canva (https://valtiachile.my.canva.site/web-valtia) y traducido a vistas separadas con navegación entre páginas.

## Comandos

```bash
nvm use 22       # Obligatorio: Astro requiere Node >=22.12.0 (el shell default es v20)
npm run dev      # Servidor de desarrollo en http://localhost:4321
npm run build    # Build de producción (usa sharp para optimizar imágenes)
npm run preview  # Previsualizar el build
```

## Idioma

- Español en respuestas y documentación
- Inglés en todo el código fuente (nombres de archivos de página en español porque son las URLs públicas: `nuestra-historia.astro` → `/nuestra-historia`)

## Clean Code

- Nombres expresivos que revelan intención
- Componentes pequeños con una sola responsabilidad
- Sin comentarios redundantes ni código muerto

## Estructura

| Capa | Ubicación |
|------|-----------|
| Páginas (rutas) | `src/pages/` |
| Componentes reutilizables | `src/components/` |
| Layouts | `src/layouts/` |
| Estilos globales y tokens | `src/styles/global.css` |
| Imágenes (optimizadas por Astro) | `src/assets/` |
| Estáticos sin procesar | `public/` |

## Reglas

### Git & Commits
- **NUNCA hacer commits sin que lo pidas explícitamente** con "hazme el commit"
- Si hago cambios, espero tu confirmación antes de commitear
- Esta regla persiste aunque hagas `/clear` o reinicies la sesión
- Remote: `git@github.com-valtia:ValtiaApp/valtia-landing.git` (alias SSH de la cuenta dpinaValtia; email local del repo: dpina@valtia.cl)

### Contenido
- El copy se extrae **exacto** de los screenshots/Canva; **nunca inventar texto**
- Si falta contenido para una vista, dejar placeholder claro y avisar, no rellenar

### General
- Formato: 2 espacios, comillas simples en JS/frontmatter, máximo 120 caracteres por línea
- Nomenclatura: PascalCase para componentes (`SectionNav.astro`), kebab-case para páginas y assets
- UI reutilizable → componente en `src/components/`; no duplicar markup entre páginas
- Cero JavaScript de cliente salvo necesidad real; preferir HTML/CSS y las capacidades de Astro

### Estilos
- Tailwind CSS v4: tokens de diseño en `@theme` dentro de `src/styles/global.css` (`--color-valtia-teal`, `--color-valtia-dark`, fuentes); utilidades custom con `@utility`
- Colores y fuentes siempre via tokens, no valores hex sueltos en las clases
- Fuentes (aproximaciones de Canva, pendiente confirmar exactas): Poppins (sans), Lora (serif/títulos), Courier Prime (mono/relatos)

### Layout responsive
- Patrón viewport-fit en cada vista: contenedor `flex min-h-dvh flex-col` + bloque central `flex-1 content-center`
- En pantallas grandes todo cabe sin scroll; en pantallas chicas se scrollea naturalmente
- Nunca alturas fijas que generen overflow

### Imágenes
- Siempre `<Image>` de `astro:assets` (nunca `<img>` con rutas de `public/` para contenido)
- Especificar `widths`/`sizes` o `densities` según el caso; `loading="eager"` solo para imágenes hero above-the-fold

### Navegación
- `<SectionNav>` presente en todas las vistas (variantes `dark`/`light` según fondo)
- Transiciones entre páginas via `<ClientRouter />` de `astro:transitions` (ya está en el Layout)

## Carpetas a ignorar en búsquedas

`.git/`, `node_modules/`, `dist/`, `.astro/`, `*.lock`
