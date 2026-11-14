# Landings con VSL · Selvaní · Fracción Pionera

Dos landings estáticas (HTML + CSS + JS en un solo archivo cada una), construidas el 2026-11-13 sobre el VSL de Jorge (vertical 4:5, 5:57).

**Desde el 2026-11-14 el video NO se sirve desde esta carpeta: vive en Panda Video.** Es el máster v14 (`exports/vsl-jorge-linea-a-v14-4x5.mp4`), idéntico imagen por imagen a v13 pero con el audio normalizado a −14 LUFS.

| Dato | Valor |
|---|---|
| `video_id` (API) | `1bedda1e-0e53-4cbe-bc02-fd89c18bb82f` |
| `v` del embed / `video_id` del SDK | `8799ea96-0d90-4146-837d-2318463fa32f` |
| `library_id` | `vz-d2e616d4-07c` |
| Perfil de player | `Selvaní · VSL Línea A (cerrado)` — Smart Autoplay, sin controles, barra de progreso ficticia |

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
- `vsl-v13-web-640.mp4` (640×800, 34 MB, nunca estuvo en git): **ya no se usa.** Era el VSL autoalojado hasta el 2026-11-14; ahora el video lo sirve Panda. Se puede borrar.

## Cómo está puesto el VSL (2026-11-14)
Cada página tiene un `<iframe class="main">` con el `src` guardado en **`data-src`**: el iframe se crea solo al primer play, así quien no ve el video no descarga nada y el Smart Autoplay de Panda arranca cuando la persona lo pidió.

Los saltos (12 capítulos en `4-sincronia`, 4 momentos en `5-modulo`) usan `PandaPlayer.setCurrentTime()` del SDK `https://player.pandavideo.com.br/api.v2.js`, que se carga también al primer play. El tiempo para resaltar el capítulo activo llega por `postMessage` (`panda_timeupdate` / `panda_progress`), no por eventos del DOM: el iframe no los emite.

**Comprobado el 2026-11-14 contra el perfil cerrado**, porque no era obvio que funcionara: `setCurrentTime(140)` movió el video de 28 s a 141,9 s y llegaron `panda_seeking` y `panda_seeked`. Importa verificarlo si alguna vez se cambia el perfil: uno restrictivo **puede hacer que el reproductor ignore las órdenes** (ya pasó con `disablePause` en las landings de miguellemus.co, 28 oct 2026). Si un día los capítulos dejan de saltar, mirar primero el perfil del player en Panda, no el JavaScript.

## En producción (2026-11-14)
Las dos landings están desplegadas en Vercel (equipo `atm-co-projects`, proyecto `selvani-fraccion-pionera`), junto a las tres anteriores:
- Sincronía: https://selvani-fraccion-pionera.vercel.app/sincronia/
- El módulo: https://selvani-fraccion-pionera.vercel.app/modulo/
- Portada con las cinco: https://selvani-fraccion-pionera.vercel.app

La carpeta de despliegue completa (con las landings 1–3 bajadas del despliegue anterior y el enlace al proyecto) vive en `_vercel/`; ahí está el procedimiento para volver a desplegar. Siguen pendientes antes de pautar: URL de Calendly (`CAL`), política de datos (`POL`), backend del formulario, og:image absoluta, pixel + CAPI.

## Auditoría de cumplimiento (2026-11-13)
Pasó por `pauta-highticket:auditor-cumplimiento`. Se aplicaron sus 4 bloqueantes y 11 menores: se quitó "lo peor que puede pasar…" y "el riesgo está resuelto por diseño"; el "100 %" quedó solo en el mecanismo y en una FAQ, siempre con la condición delante; se agregó el aviso de tratamiento de datos bajo el formulario; "Liquidez real" pasó a "Transferible" sin "cuando decidas"; restaurante y piscina condicionados a las áreas comunes; la cifra pasó de "98 · 62" a "62 disponibles" (70 para terceros); disclaimer repetido dentro de "Lo que incluye" y más grande en el pie; sin "seguridad/seguro" como gancho; sin FOMO.

## Pendiente para publicar de verdad
1. URL de Calendly: variable `CAL` al inicio del `<script>` de cada página (el botón "Agendar directo" aparece solo si existe).
2. URL de la política de tratamiento de datos: variable `POL` junto a `CAL` (el enlace bajo el formulario aparece solo si existe). Sin política publicada, Meta puede rechazar el destino.
3. Formulario sin backend: valida y agradece, no envía. Mientras no exista endpoint, el "Ya tenemos tus datos" es falso: conectar a Kommo / n8n antes de pautar.
4. `og:image` es ruta relativa; al desplegar, cambiar a URL absoluta del dominio final.
5. Pixel de Meta + CAPI.
6. Confirmar 70/62 fracciones y que el VSL v13 es la versión aprobada por Jorge. El VSL sí dice "usas el restaurante, nadas en la piscina" sin condicionar a las áreas comunes; revisar con Jorge.

## Repo en GitHub (2026-11-14)
`mlemus27/selvani-landings`, **privado**. Contiene solo esta carpeta, con su historia. El repo de verdad sigue siendo el de la Mac (su raíz es la carpeta de usuario y mezcla Selvaní con Oficina Hermes, que incluye la IP del VPS y el inventario de puertos: eso NO sube a ningún servidor).

Para actualizar GitHub después de comitear aquí, se recorta esta carpeta y se empuja ese corte:
```bash
cd ~ && git branch -D selvani-landings-solo 2>/dev/null
git -c core.quotePath=false subtree split -P "Documents/Claude Code/02 ATM/Clientes/Selvaní/Selva : ADN de Marca/landings" -b selvani-landings-solo
git push selvani-landings selvani-landings-solo:main
```
`core.quotePath=false` es obligatorio: sin eso `subtree` compara la ruta escapada (`Selvan303255`) con la literal y se cae con *assertion failed* por la «í» de Selvaní.

## Probar en local
```bash
python3 -m http.server 8765 --directory landings
```
y abrir `http://localhost:8765/4-sincronia/` o `/5-modulo/`.

## Artifacts (privados, versión con video ligero de 13 MB)
- Landing 4 · Sincronía: https://claude.ai/artifact/M8GE8JaVw9Sjh3bKoGA4qb
- Landing 5 · El módulo: https://claude.ai/artifact/LZzFGXNMYZSiXde4Z4LGLW
Hay que compartirlos desde el menú de la página antes de que Jorge/Felipe puedan abrirlos. La fuente editable es esta carpeta, no el Artifact.
