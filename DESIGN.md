# Design System — Perfil de GitHub de SloKBac

Sistema de diseño del repositorio de perfil (`JuanP-a/JuanP-a`). Documenta los
tokens, reglas y estructura para que el perfil se mantenga coherente y no se
convierta en una colección de widgets sin criterio.

## La cosa memorable

> **"Un hacker de terminal que entrega full-stack **seguro**."**

Toda decisión visual sirve a esa frase. Si algo no la refuerza, se saca.

## Paleta (tokens)

| Token | Hex | Uso |
|:--|:--|:--|
| `bg` | `#0d1117` | Fondo de banners. Nunca `#000000` (rompe con el negro de GitHub). |
| `accent` | `#39FF14` | Verde neón — acento primario (typing, badges clave). |
| `accent-2` | `#22D3EE` | Cian — acento secundario (segundo color de gradiente, links). |
| `accent-3` | `#FF00FF` | Magenta — uso **raro** (p. ej. el fuego del streak). |
| `text` | `#c9d1d9` | Texto normal sobre fondo oscuro. |
| `muted` | `#8b949e` | Texto secundario. |

**Regla:** máximo **2 acentos visibles a la vez** en una misma sección. El
magenta no se usa como color de texto (solo detalles gráficos).

## Tipografía

- **JetBrains Mono** → datos, código, marcadores de sección (`$`), el bloque `console`.
- **Sans del sistema (GitHub)** → prosa y tablas.
- Los headings de sección usan el prefijo `$` como firma de "terminal".

## Estructura (zonas)

El perfil se organiza en **3 zonas** para minimizar scroll:

1. **Hero / identidad** — banner, rol, typing, stack, contacto.
2. **Trabajo** — proyectos (tabla).
3. **Actividad** — métricas + serpiente de contribuciones.
4. **Detalle** — ciberseguridad, dentro de `<details>` (se abre al clic).

## Reglas de composición

- **Un solo hero.** Los banners grandes (`capsule-render`) solo en el header y
  en un footer fino.
- **≤ 3 zonas de contenido** + detalle colapsado. No apilar widgets.
- **Sin redundancia:** si dos widgets muestran lo mismo (p. ej. `streak` y
  `metrics`), queda **uno**.
- **Todo lo importante, arriba:** rol + proyectos deben verse sin scroll.
- Números y datos técnicos en monoespaciada.

## Accesibilidad (WCAG 2.2 AA)

- **`alt` en TODAS las imágenes.** Escritas descriptivas; imágenes puramente
  decorativas con `alt=""`.
- **Contraste verificado:**

  | Par | Ratio | |
  |:--|--:|:--|
  | `#39FF14` / `#0d1117` | 13.96:1 | AA |
  | `#22D3EE` / `#0d1117` | 10.47:1 | AA |
  | `#c9d1d9` / `#0d1117` | 12.26:1 | AA |
  | `#8b949e` / `#0d1117` | 6.15:1 | AA |
  | `#FF00FF` / `#0d1117` | 6.03:1 | AA |

- **Headings jerárquicos:** secciones con `##` (no `###` huérfanos).
- **Motion:** `typing-svg` y `snake` animan en loop y **no** se puede aplicar
  `prefers-reduced-motion` en GitHub (se renderizan como `<img>`). El texto del
  typing duplica información que ya está en texto plano; la snake es decorativa.

## Widgets (todas gratis, sin costo)

| Función | Servicio | Hosting |
|:--|:--|:--|
| Banner | [capsule-render](https://github.com/kyechan99/capsule-render) | Vercel |
| Typing | [readme-typing-svg](https://github.com/DenverCoder1/readme-typing-svg) | Vercel |
| Stack | [skillicons.dev](https://skillicons.dev) | propio |
| Badges/contacto | [shields.io](https://shields.io) | propio |
| **Métricas** | [lowlighter/metrics](https://github.com/lowlighter/metrics) | **self-hosted** (Action) |
| Visitas | [komarev](https://komarev.com/ghpvc/) | propio |
| **Snake** | [Platane/snk](https://github.com/Platane/snk) | **self-hosted** (Action) |

> Los self-hosted no dependen de Vercel → no dan `402`.

## Automatización

- `.github/workflows/snake.yml` — regenera la serpiente a diario.
- `.github/workflows/metrics.yml` — regenera `github-metrics.svg` a diario.

## Convenciones de edición

- Cambios de estilo van en `README.md` y `README.es.md` **en el mismo commit**
  (deben quedar espejados).
- Mantener la paleta y las reglas de arriba; si algo las rompe, actualizar este
  archivo primero.
