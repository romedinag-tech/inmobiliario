# Rediseño gráfico institucional — checklist y pruebas (anti-salto de pasos)

Regla: NO marcar una fase [x] sin pegar la evidencia de su PRUEBA. Golden master =
solo presentación; los datos (56 figuras) no cambian.

## Baseline golden-master (medido antes de tocar nada)
`figuras:56 · canvases:20 · svgs:24 · kpis:39 · tablas:1 · tabs:10 · cargando:false`

## PRUEBA ESTÁNDAR (correr en preview_eval al cerrar cada fase)
```js
(()=>{const cs=getComputedStyle(document.body);
return {figuras:document.querySelectorAll('canvas,svg,.chart,[class*="map"]').length,
 canvases:document.querySelectorAll('canvas').length, kpis:document.querySelectorAll('.kpi').length,
 tablas:document.querySelectorAll('table').length, cargando:!!document.body.textContent.match(/Cargando|cargando/),
 h1font:getComputedStyle(document.querySelector('h1')||document.body).fontFamily.slice(0,22),
 bodyFont:cs.fontFamily.slice(0,16)};})()
```
Criterio de paso: `figuras>=56`, `canvases==20`, `kpis==39`, `cargando==false`, **0 errores de consola**.

---

## Fase 0 — Fundación (tokens + tema claro) ✅ HECHO
- [x] tokens.css fuente única, cargado primero — *evidencia: token_paper #FBFBFD, token_navy #16365a, hexSueltos=1 (el propio tokens.css)*
- [x] Tema claro institucional por defecto — *bodyBg rgb(251,251,253); dark:false*
- [x] Fuentes Source Serif 4 + Inter + tabular — *--font-display 'Source Serif 4'*
- [x] Paletas de dato colorblind-safe documentadas — *div/seq/cat en tokens.css*
- [x] Oscuro re-estilizado sobrio (sin neón) — *dark_bg #0D1E33, navy #4C93F5*
- [x] PRUEBA: figuras 56 (claro y oscuro), 0 errores consola. Caché theme.css?v=2.

## Fase 1 — Sistema de Figura + jerarquía tipográfica  ✅ (tipografía) / eyebrow→Fase 2
- [x] H1/H2/H3 de sección usan --font-display (serif) — *h1font/h2font/figTitleFont = "Source Serif 4"*
- [~] Componente Figura: clases .eyebrow/.fig-src DEFINIDAS; título serif + bajada ya estilados.
      **Aplicación por-figura del eyebrow(fuente)+microlínea → movida a Fase 2 (marco de figura).**
- [x] KPIs en cifras tabulares grandes — *tabular-nums en .kpi .v (heredado F1), .kpi .v serif-navy*
- [x] Salto display→cuerpo→caption obvio; interlineado 1.5 en tablas/.lead/.chartbox p
- [x] PRUEBA estándar OK — *figuras:56, canvases:20, kpis:39, tablas:1, cargando:false, 0 errores consola, h1 32.8px serif*

## Fase 2 — Layout editorial + nav sticky + confianza  ✅ HECHO
- [x] Figura en --surface con hairline (.chartbox ya) + MARCO uniforme (22 eyebrows + 22 fig-src)
- [x] Nav STICKY con activa en --accent (#1F6FEB) — *navSticky:sticky, navActiveBorder rgb(31,111,235)*
- [x] Footer institucional + metodología en drawer colapsable — *drawer:true, texto íntegro 2302 chars*
- [x] Callout "Estudios a medida" tarjeta premium (borde --navy) — *callout:true*
- [x] Skeletons ya existían (F1) + .note tokenizado (quitó 3 hex sueltos)
- [x] PRUEBA estándar OK — *figuras:56, canvases:20, kpis:39, cargando:false, 0 errores consola*

## Fase 3 — Restyle gráficos (Chart.js con tokens)  ✅ HECHO
- [x] Chart.defaults desde tokens: color --ink-mid, grid --line, tooltip --surface/--line/--ink
- [x] Constantes NAVY/OR/… en app.js leen tokens (cssv); + CAT/SEQ arrays; NSE_COLORS → secuencial azul CB-safe; ramp RdYlGn rojo-verde → RdBu CB-safe
- [x] Tooltips uniformes (backgroundColor --surface, borde --line, cifras --ink)
- [~] Etiquetado directo / selección --accent: base lista (ACCENT disponible); refinamiento por-gráfico → Fase 5 si hace falta
- [x] PRUEBA estándar OK — *figuras:56, canvases:20, kpis:39, cargando:false, usesOldNavy:FALSE, 7 charts con #16365a/#C55A11, 0 errores consola. app.js?v=26*

## Fase 4 — Mapas coropléticos + O-D  ✅ HECHO
- [x] Coropléticos: selección/hover → --accent (#1F6FEB, 0 usos de #1f4e79); NSE secuencial CB-safe; leyenda tokenizada
- [x] Densificación/expansión: colDE = RdBu colorblind-safe (rojo=expansión, azul=densificación)
- [x] O-D: flecha/par → accent; **clic conservado** (odFlowMap intacto, solo cambió color)
- [x] Leyenda + .info tokenizados (--surface/--line, cifras tabulares) — *legendBg #FFF, borde #E3E8EF*
- [x] PRUEBA OK — *figuras:60 (≥56), kpis:39, cargando:false, 0 #1f4e79 en app.js, 0 errores consola. app.js?v=27*

## Fase 5 — AA + responsive + verificación final  ✅ HECHO
- [x] :focus-visible (--focus) en toda la app; reduced-motion; **aria-label en 22 figuras** (role=group)
- [x] Responsive 390/834/1440 SIN scroll horizontal — *390 y 834: overflowBy 0; .layout→columna móvil, tabs scroll, controles min-width:0*
- [x] display=swap (fonts) + skeletons (reservan altura). Carga diferida ya en iframes.
- [x] COMPUERTA FINAL: **hexSueltos inline=0** (solo 1 en theme.css = tokens oscuros, legítimo); figuras:60(≥56); kpis:39; cargando:false; 0 errores consola

## Checklist final
- [ ] Tema claro institucional; tokens.css única fuente.
- [ ] Autoridad tipográfica (serif+sans+tabular).
- [ ] Sistema de Figura uniforme en todas las secciones.
- [ ] Nav sticky + footer + metodología (drawer) + callout servicio + skeletons.
- [ ] Gráficos unificados colorblind-safe; cero colores por defecto.
- [ ] Mapas consistentes y accesibles.
- [ ] AA + responsive + reduced-motion.
- [ ] Golden master: toda figura renderiza los mismos datos que el baseline.
