---
name: sdlc-soporte
description: "Prompts AI-SDLC de soporte y mesa de ayuda. Úsala en soporte a usuarios: triage de tickets, diagnóstico y respuesta de un incidente de soporte, artículos de base de conocimiento, matriz de escalamiento y SLA, tendencias de tickets o auditoría de la base de conocimiento."
license: CC-BY-4.0
---

# Fase AI-SDLC 16 — Soporte y mesa de ayuda

Esta skill agrupa los prompts de la fase **Soporte y mesa de ayuda** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 16.1 — Triage y clasificación de tickets de soporte
- Archivo: [references/16-01-triage-tickets-soporte.md](references/16-01-triage-tickets-soporte.md)
- Cuándo usarlo: al recibir uno o varios tickets nuevos (soporte, mesa de ayuda, canal de incidentes de cliente) que necesitan severidad, SLA y equipo asignados antes de que alguien intervenga.
- Entradas: texto y metadatos del ticket o lote de tickets (título, descripción, reportante, timestamp, entorno, adjuntos/logs si existen), tabla o política de SLA vigente por severidad, acceso de lectura al historial de tickets o base de conocimiento para detectar dupli…
- Autonomía permitida: A0 — Analizar (lectura del ticket, búsqueda de duplicados/conocidos); A1 — Proponer (severidad, SLA y equipo propuestos); nunca A2/A3 — este prompt no asigna el ticket, no cambia su estado ni ejecuta ninguna acción sobre el sistema de tickets
- Detente si: detener y pedir más información si el ticket no tiene datos suficientes para determinar severidad (sin descripción, sin impacto ni entorno indicado) — no inventar una severidad plausible; marcar como "posible duplicado, no confirmado" si la coincidencia con un ticket previo no es clara, en vez de d…
- Siguiente: `16-02-diagnostico-respuesta-incidente-soporte`, `11-04-incident-response` (skill `sdlc-operaciones`)

### 16.2 — Diagnóstico y primera respuesta a incidente de soporte
- Archivo: [references/16-02-diagnostico-respuesta-incidente-soporte.md](references/16-02-diagnostico-respuesta-incidente-soporte.md)
- Cuándo usarlo: inmediatamente después de que un ticket fue clasificado y priorizado por `16-01-triage-tickets-soporte`.
- Entradas: ticket ya triado con prioridad y severidad asignadas (salida de `16-01`), pasos de reproducción reportados por el usuario, entorno afectado, evidencia disponible (logs, capturas, mensajes de error), acceso de lectura a incidentes conocidos y artículos de KB,…
- Autonomía permitida: A0 — Analizar (diagnóstico: reproducir, aislar causa probable, revisar KB); A1 — Proponer (redactar la primera respuesta al usuario); nunca A2/A3 — este prompt no ejecuta ni publica cambios en el sistema
- Detente si: detener y escalar a un prompt de ejecución/ingeniería (`03-01-incidentes-github` o `11-01-troubleshooting`) si el diagnóstico confirma un bug de código que requiere cambio; detener y escalar a `11-04-incident-response` si se trata de un incidente de producción con impacto significativo; si el probl…
- Siguiente: `16-01-triage-tickets-soporte`, `03-01-incidentes-github` (skill `sdlc-incidentes`), `11-01-troubleshooting` (skill `sdlc-operaciones`), `11-04-incident-response` (skill `sdlc-operaciones`)

### 16.3 — Artículo de base de conocimiento desde ticket resuelto
- Archivo: [references/16-03-articulo-base-conocimiento.md](references/16-03-articulo-base-conocimiento.md)
- Cuándo usarlo: después de que un ticket se resuelve y el patrón (síntoma + causa + solución) es probable que se repita, evitando que el siguiente agente de soporte tenga que re-diagnosticar el mismo caso desde cero.
- Entradas: ticket resuelto con síntoma reportado, causa raíz confirmada (propia o proveniente del diagnóstico de `16-02`), pasos de solución aplicada y validada, sistema/producto/versión afectado, audiencia destino del artículo
- Autonomía permitida: A1 — Proponer (redactar el artículo de KB como borrador); nunca A2/A3 — publicar el artículo en el sistema de KB de producción requiere revisión y aprobación humana explícita fuera de este prompt
- Detente si: detener y escalar si el ticket no tiene causa raíz confirmada (solo síntoma resuelto sin diagnóstico) — no inventar una causa plausible; si la solución aplicada no fue validada como efectiva (ticket cerrado sin confirmación del usuario o de QA), marcar el artículo completo como borrador de baja con…
- Siguiente: `16-02-diagnostico-respuesta-incidente-soporte`

### 16.4 — Matriz de escalamiento y SLA por severidad
- Archivo: [references/16-04-matriz-escalamiento-sla.md](references/16-04-matriz-escalamiento-sla.md)
- Cuándo usarlo: al establecer por primera vez la política de soporte de un producto/equipo, o al revisarla periódicamente (cambio de capacidad del equipo, nuevos SLAs contractuales, incidentes recientes que revelaron huecos en la cadena de escalamiento).
- Entradas: catálogo de tipos de incidentes/tickets conocidos (si existe), capacidad real del equipo de soporte (headcount, horario de cobertura, existencia de on-call), SLAs contractuales ya vigentes con clientes (si aplica), definiciones de severidad usadas actualmente…
- Autonomía permitida: A0 — Analizar (relevar SLAs y capacidad existentes); A1 — Proponer (la matriz de severidad, SLA y cadena de escalamiento); nunca A2/A3 — la matriz requiere aprobación humana explícita antes de adoptarse como política oficial de soporte
- Detente si: detener y escalar a un humano si no hay información real de capacidad del equipo (headcount, horario de cobertura) — no fabricar una matriz de SLA sin verificar que el equipo puede sostenerla; señalar como propuesta de baja confianza si existen SLAs contractuales con clientes que no pudieron confir…
- Siguiente: `16-01-triage-tickets-soporte`

### 16.5 — Análisis de tendencias y causas raíz agregadas de tickets
- Archivo: [references/16-05-analisis-tendencias-tickets.md](references/16-05-analisis-tendencias-tickets.md)
- Cuándo usarlo: periódicamente (mensual o trimestral) sobre un lote de tickets que ya fueron atendidos y cerrados individualmente vía `16-02`, como ejercicio retrospectivo para alimentar decisiones de producto e ingeniería.
- Entradas: export o acceso de lectura al lote de tickets resueltos del período a analizar (idealmente con categoría, resumen, resolución y tiempo de resolución de cada uno), rango de fechas o período a cubrir, taxonomía de categorías existente si el equipo ya usa una
- Autonomía permitida: A0 — Analizar (lectura y categorización agregada del lote); A1 — Proponer (recomendar iniciativas de ingeniería o documentación); nunca A2/A3 — este prompt no crea issues, no despliega documentación ni ejecuta cambios de producto
- Detente si: detener y escalar si el lote de tickets disponible es demasiado pequeño o no tiene campos mínimos (categoría, resumen, resolución) para sustentar un patrón agregado — no inventar categorías ni causas raíz sin evidencia de al menos varios tickets repetidos; señalar como hallazgo de baja confianza cu…
- Siguiente: `02-04-triage-backlog-github` (skill `sdlc-analisis`), `10-01-documentacion-tecnica` (skill `sdlc-documentacion`), `16-06-auditoria-base-conocimiento`

### 16.6 — Auditoría de salud de la base de conocimiento de soporte
- Archivo: [references/16-06-auditoria-base-conocimiento.md](references/16-06-auditoria-base-conocimiento.md)
- Cuándo usarlo: periódicamente (ej. trimestral) como mantenimiento de la KB, o cuando el equipo de soporte reporta que los artículos existentes ya no reflejan el producto actual o que cuesta encontrar la respuesta correcta.
- Entradas: inventario de artículos de la KB (título, fecha de última actualización, categoría, métricas de uso/vistas si existen), versión actual del producto o changelog reciente, categorías de tickets recurrentes (de `16-05` si existe, o el historial de tickets direct…
- Autonomía permitida: A0 — Analizar (staleness, duplicados, cobertura, uso); A1 — Proponer (qué actualizar, fusionar, archivar o crear); nunca A2/A3 — la publicación o eliminación real de artículos requiere revisión y ejecución humana del responsable de la KB
- Detente si: detener y señalar si no hay fecha de última actualización disponible para evaluar staleness — no asumir que un artículo está vigente solo porque no hay evidencia de que esté desactualizado; si no hay métricas de uso, limitar el análisis de "sin uso" a lo que pueda inferirse de otra forma y declarar…
- Siguiente: `16-03-articulo-base-conocimiento`, `16-05-analisis-tendencias-tickets`

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
