# CV — Sebastian Asprino

Currículum vitae / portafolio web de Sebastian Asprino construido con [Astro](https://astro.build).
El contenido vive en un único archivo de datos (`cv.json`, con una estructura inspirada en
[JSON Resume](https://jsonresume.org/schema)) y las páginas lo renderizan como HTML estático.

> Estado: en desarrollo. Los datos del CV (experiencia, educación, certificados, habilidades,
> idiomas, proyectos) ya están cargados en `cv.json`; las secciones visuales se están construyendo
> componente por componente.

## Características

- Sitio estático sin JavaScript en el cliente.
- Contenido separado de la presentación: editar `cv.json` actualiza la página.
- Metadatos SEO, Open Graph y Twitter generados a partir de los datos del CV.
- Estilos preparados para impresión (`@media print`), para exportar el CV a PDF desde el navegador.
- Verificación de tipos con `astro check` (configuración `strict` de TypeScript) antes de cada build.

## Stack

- Astro 4 + TypeScript (strict)
- CSS plano con estilos con alcance por componente
- [Bun](https://bun.sh) como gestor de paquetes (`bun.lockb`)

## Estructura

```text
.
├── cv.json                 # Fuente única de datos del CV
├── public/                 # Archivos estáticos (favicon)
├── src/
│   ├── pages/index.astro   # Página principal: <head> con SEO y estilos globales
│   └── sections/
│       ├── section.astro   # Contenedor genérico de sección con título opcional
│       └── basics.astro    # Sección de datos básicos (en construcción)
├── astro.config.mjs
└── tsconfig.json
```

## Uso

```sh
bun install       # Instala dependencias
bun run dev       # Servidor de desarrollo en http://localhost:4321
bun run build     # astro check + build estático en ./dist
bun run preview   # Sirve el build localmente
```

## Editar el contenido

Modificá `cv.json`. Las secciones principales son `basics`, `work`, `volunteer`, `education`,
`certificates`, `skills`, `languages`, `projects`, `references` y `awards`. Los campos de
`basics` (`name`, `label`, `summary`, `url`, `image`) alimentan el título y los metadatos de la página.

## Despliegue

`bun run build` genera un sitio estático en `dist/`, publicable en cualquier hosting estático
(Vercel, Netlify, GitHub Pages, Cloudflare Pages, etc.).

## Integración continua

`.github/workflows/ci.yml` instala dependencias con Bun y ejecuta `bun run build` (que incluye
`astro check`) en cada push y pull request a `master`.
