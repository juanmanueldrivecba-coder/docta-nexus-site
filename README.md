# Docta Nexus — Sitio web

Sitio estatico multipagina (HTML + CSS, sin frameworks ni build step).

## Estructura de carpetas

El repositorio esta organizado en carpetas para facilitar la edicion, pero
**las URLs publicas del sitio no cambian**: Render las reescribe internamente
via `render.yaml` (ver seccion mas abajo), asi que `/paid-media.html` sigue
siendo `/paid-media.html` aunque el archivo fisico viva en otra carpeta.

- `index.html`, `soluciones.html`, `ai-product-lab.html`, `casos-de-estudio.html`,
  `blog.html`, `sobre-nosotros.html`, `como-funciona-modelo-growth-tech.html`,
  `contacto.html`, `faq.html` — paginas "hub" del menu, quedan en la raiz.
- `blog/` — los articulos de blog (`blog-*.html`).
- `casos/` — el detalle de cada caso de estudio (`casos-*.html`).
- `desarrollos/` — el detalle de cada producto de AI Product Lab (`desarrollos-*.html`).
- `soluciones/` — paginas de servicio. A su vez dividida en las mismas
  categorias del mega-menu "Soluciones":
  - `soluciones/estrategia-consultoria/`
  - `soluciones/produccion-creativa/`
  - `soluciones/activacion-medios/`
  - `soluciones/datos-medicion/`
  - `soluciones/planificacion-control/`
  - Sueltas en `soluciones/` (no pertenecen a ninguna categoria del menu
    nuevo): `shadow-ia-enterprise.html`, `crm-agentes-ia.html`.
- `assets/` — logos, favicon, imagen OG, `style.css`.
- `sitemap.xml`, `robots.txt` — SEO tecnico (usan URLs absolutas, no
  necesitan tocarse si se mueven archivos).

## Como agregar o mover una pagina

1. Crea o mueve el archivo `.html` a la carpeta que corresponda.
2. Todos los links internos del sitio usan rutas absolutas (`/pagina.html`,
   `/assets/style.css`), nunca relativas — por eso un archivo funciona igual
   sin importar en que carpeta este.
3. Si el archivo es nuevo, agrega su URL a `sitemap.xml`.
4. Si moves un archivo que ya existia (cambia de carpeta pero no de URL
   publica), agrega una regla en `render.yaml` bajo `routes`:
   ```yaml
   - type: rewrite
     source: /nombre-de-archivo.html
     destination: /carpeta/nombre-de-archivo.html
   ```

## Deploy en Render (Static Site)

1. Subir este repo a GitHub.
2. En Render: New > Static Site > conectar el repo.
3. Build Command: dejar vacio.
4. Publish Directory: `.` (raiz del repo).
5. Deploy. Render lee `render.yaml` automaticamente y aplica las reglas
   de rewrite para que las URLs publicas sigan siendo las de siempre.

## Dominio propio (doctanexus.com)

En Render, agregar el dominio custom en Settings > Custom Domains,
y apuntar el DNS del dominio (en el proveedor donde este registrado)
segun las instrucciones que Render indique (CNAME o registros A).
