# Web del GEA 

Organización y guías de uso

## Idiomas (ES / EN)

El contenido está separado por idioma: `content/es/` (raíz del sitio) y `content/en/` (`/en/`). Las carpetas en inglés tienen otro nombre
(`research-lines`, `members`, `projects`, `publications`, `theses`, `scholarships`, `news`, `teaching`, `gallery`, `links`), pero se comportan igual.
Para que el selector ES/EN lleve a la página equivalente, ambas versiones deben compartir el mismo `translationKey` en el front matter
(ya está en las páginas de ejemplo). Si una página no tiene traducción, el selector lleva a la portada del otro idioma.
Textos fijos de la interfaz: `i18n/es.toml` y `i18n/en.toml`. Menús, roles y datos de contacto por idioma: `hugo.toml`.

 
## Contenido  
Todo vive en `content/es/` y `content/en/` como archivos `.md`. 

| Qué | Dónde | Cómo |
|---|---|---|
| Novedad | `content/es/novedades/AAAA-MM-DD-titulo.md` (y `content/en/news/…`) | copiar una existente |
| Integrante | `content/es/integrantes/apellido.md` (y `content/en/members/…`) | campos `rol`, `cargo`, `foto`, `links` |
| Proyecto | `content/es/proyectos/nombre.md` | `estado: activo` o `finalizado` |
| Línea | `content/es/lineas/nombre.md` | `weight` define el orden |
| Fotos | `static/img/integrantes/` | referenciar como `/img/integrantes/foto.jpg` |

Los **enlaces a perfiles externos** (CONICET, ORCID, Scholar, CV) se listan en `links:` del front matter de cada integrante; cada persona agrega los suyos.

Se recomienda proteger `main` y que los cambios entren por Pull Request.

### Editar desde GitHub (sin instalar nada)
Desde GitHub: **Add file → Create new file** (o el lápiz para editar) y *Commit*. Cloudflare publica solo en ~1 minuto.

### Probar local
- Descargar Hugo
- Descargar repositorio
- Editar el contenido
- Correr hugo para compilar y generar web
`hugo server` (Hugo extended >= 0.139).


## Publicar
1. Subir el repo a GitHub y reemplazar `params.repo` en `hugo.toml`.
2. Cloudflare → Workers & Pages → Create → Pages → conectar el repo.
   Build command: `hugo --minify` · Output: `public` · Variable `HUGO_VERSION=0.147.0`.
3. Pages → Custom domains → `gea.ing.unrc.edu.ar`.
 

## Publicaciones (siguiente etapa)
La página ya lee `data/publicaciones.json` (`year`, `title`, `authors[]`, `venue`, `url`).
Después se agrega un workflow en `.github/workflows/` con `schedule: cron` que corre el scraper y hace commit solo si `git diff --quiet` detecta cambios.
