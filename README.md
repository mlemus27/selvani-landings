# Landings con VSL · Selvaní · Fracción Pionera

Dos landings estáticas (HTML + CSS + JS en un solo archivo cada una), construidas el 2026-11-13 sobre el VSL v13 de Jorge (`exports/vsl-jorge-linea-a-v13-4x5.mp4`, vertical 4:5, 5:57).

| Carpeta | Concepto | Firma |
|---|---|---|
| `4-sincronia/` | Tema Profundo (Línea A). El VSL vertical queda fijo a la izquierda y el guion por capítulos se ilumina a medida que avanza el video; tocar un capítulo salta a ese minuto. | Guion sincronizado con el video + hilo de progreso. |
| `5-modulo/` | Tema Crudo editorial. Carta de venta larga con el VSL como primera prueba y un diagrama del módulo que se arma al bajar: 5 fracciones, 4 = punto de equilibrio, fiducia, construcción, y la rama de los seis meses. | Diagrama interactivo del mecanismo (scrollytelling). |

## Copy
Adaptado del copy aprobado de las landings 1 y 2 (2026-10-29) y alineado con las **precisiones legales de Jorge del 2026-11-05** (`design-system/brand-book.md`): fiducia "se reserva" y "los recursos solo se usan al punto de equilibrio"; "ingresos mensuales por operación turística"; "rendimientos" en vez de "intereses"; seis meses = plazo de comercialización; Finanfuturo como aliado de back office. Sin precio, sin porcentajes de rentabilidad, sin "hotel boutique". Jorge se presenta como "uno de los desarrolladores" (así lo dice el VSL v13).

Cifra viva usada: **62 fracciones disponibles** (de 70 para terceros; dato del 2026-11-05). Confirmar con el cliente antes de publicar.

## Tipografía
Zalando Sans y Zalando Sans Expanded desde Google Fonts (la fuente oficial del manual; antes se usaba Jost como sustituto). Fallback: Jost, Helvetica, Arial.

## Medios (`_media/`)
- Fotos reales del territorio (Tomás de la Ossa, sep 2025), enderezadas y sin metadatos, en 1800 px y 900 px.
- Logos del design system (`lockup-*`, `isotipo-*`).
- `teaser-agua.mp4` y `teaser-peninsula.mp4`: loops mudos de 10 s recortados de los drones DJI (4:5) para el hero antes de dar play.
- `vsl-poster*.jpg`, `poster-*.jpg`: fotogramas fijos.
- **No están en git** (tamaño): `vsl-v13-web-640.mp4` (640×800, 34 MB, el que usan las dos páginas). Se regenera así desde la carpeta del proyecto:

```bash
ffmpeg -i exports/vsl-jorge-linea-a-v13-4x5.mp4 -c:v libx264 -preset slow -crf 27 -vf scale=640:800 -pix_fmt yuv420p -movflags +faststart -c:a aac -b:a 80k -ac 2 landings/_media/vsl-v13-web-640.mp4
```

## Auditoría de cumplimiento (2026-11-13)
Pasó por `pauta-highticket:auditor-cumplimiento`. Se aplicaron sus 4 bloqueantes y 11 menores: se quitó "lo peor que puede pasar…" y "el riesgo está resuelto por diseño"; el "100 %" quedó solo en el mecanismo y en una FAQ, siempre con la condición delante; se agregó el aviso de tratamiento de datos bajo el formulario; "Liquidez real" pasó a "Transferible" sin "cuando decidas"; restaurante y piscina condicionados a las áreas comunes; la cifra pasó de "98 · 62" a "62 disponibles" (70 para terceros); disclaimer repetido dentro de "Lo que incluye" y más grande en el pie; sin "seguridad/seguro" como gancho; sin FOMO.

## Pendiente para publicar de verdad
1. URL de Calendly: variable `CAL` al inicio del `<script>` de cada página (el botón "Agendar directo" aparece solo si existe).
2. URL de la política de tratamiento de datos: variable `POL` junto a `CAL` (el enlace bajo el formulario aparece solo si existe). Sin política publicada, Meta puede rechazar el destino.
3. Formulario sin backend: valida y agradece, no envía. Mientras no exista endpoint, el "Ya tenemos tus datos" es falso: conectar a Kommo / n8n antes de pautar.
4. `og:image` es ruta relativa; al desplegar, cambiar a URL absoluta del dominio final.
5. Pixel de Meta + CAPI.
6. Confirmar 70/62 fracciones y que el VSL v13 es la versión aprobada por Jorge. El VSL sí dice "usas el restaurante, nadas en la piscina" sin condicionar a las áreas comunes; revisar con Jorge.

## Probar en local
```bash
python3 -m http.server 8765 --directory landings
```
y abrir `http://localhost:8765/4-sincronia/` o `/5-modulo/`.

## Artifacts (privados, versión con video ligero de 13 MB)
- Landing 4 · Sincronía: https://claude.ai/artifact/M8GE8JaVw9Sjh3bKoGA4qb
- Landing 5 · El módulo: https://claude.ai/artifact/LZzFGXNMYZSiXde4Z4LGLW
Hay que compartirlos desde el menú de la página antes de que Jorge/Felipe puedan abrirlos. La fuente editable es esta carpeta, no el Artifact.
