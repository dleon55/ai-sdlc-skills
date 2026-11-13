---
name: sdlc-backoffice-ingenieria
description: "Prompts AI-SDLC de back office de ingeniería. Úsala en gestión del equipo de ingeniería: onboarding y offboarding técnico, evaluación de herramientas y licencias, capacidad del equipo, renovación de proveedores, reporte de estado a interesados, revisión posterior al lanzamiento o retrospectiva de sprint."
license: CC-BY-4.0
---

# Fase AI-SDLC 17 — Back office de ingeniería

Esta skill agrupa los prompts de la fase **Back office de ingeniería** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 17.1 — Checklist de onboarding técnico
- Archivo: [references/17-01-onboarding-tecnico.md](references/17-01-onboarding-tecnico.md)
- Cuándo usarlo: al incorporar un nuevo integrante al equipo de ingeniería, antes o durante su primer día.
- Entradas: rol y seniority del nuevo integrante, stack tecnológico y herramientas del equipo (repos, proveedor cloud, herramientas de CI/CD, gestor de secretos), nivel de acceso requerido por el rol, fecha de inicio, mentor/buddy asignado si existe, documentación intern…
- Autonomía permitida: A0 — Analizar (relevar rol, stack y accesos existentes del equipo); A1 — Proponer (el checklist de accesos, herramientas y documentación a revisar); nunca A2/A3 — este prompt no crea cuentas, no otorga permisos ni ejecuta cambios en sistemas de identidad o acceso
- Detente si: detener y pedir clarificación si no se especifica el rol o el stack del equipo — no fabricar un checklist genérico sin contexto; escalar a quien tenga permisos IAM antes de que se otorgue cualquier acceso listado; si falta información sobre el gestor de secretos o la política de acceso mínimo del e…
- Siguiente: `17-02-offboarding-tecnico`

### 17.2 — Checklist de offboarding técnico
- Archivo: [references/17-02-offboarding-tecnico.md](references/17-02-offboarding-tecnico.md)
- Cuándo usarlo: en cuanto se confirma la fecha de salida de un integrante del equipo (renuncia, despido, fin de contrato, cambio de equipo con pérdida de accesos), idealmente con antelación suficiente para planificar la transferencia de conocimiento antes del último día.
- Entradas: rol de la persona que deja el equipo y accesos/sistemas conocidos a los que tenía acceso, servicios/repositorios/rotaciones de on-call de los que es owner o mantenedor, fecha de salida confirmada, lista de sistemas de la organización que gestionan accesos (re…
- Autonomía permitida: A1 — Proponer (genera el checklist de revocación, transferencia y verificación); nunca A2/A3 — la revocación real de accesos requiere ejecución humana con permisos de administración sobre cada sistema (IAM, SSO, gestor de secretos, CI/CD), y debe completarse antes o el mismo día de la fecha de salida
- Detente si: detener y escalar si no se conoce la lista completa de accesos o sistemas a los que la persona tenía acceso — señalarlo explícitamente como riesgo residual en vez de asumir una lista completa; detener si no hay fecha de salida confirmada y usar ese hueco como bloqueante para fijar plazos concretos…
- Siguiente: `17-01-onboarding-tecnico`

### 17.3 — Evaluación y decisión de adopción de herramienta/licencia
- Archivo: [references/17-03-evaluacion-herramienta-licencia.md](references/17-03-evaluacion-herramienta-licencia.md)
- Cuándo usarlo: antes de adoptar formalmente una nueva herramienta, SaaS o librería paga que implique costo recurrente o dependencia de un proveedor externo.
- Entradas: nombre de la herramienta/servicio candidato, problema o necesidad que resuelve, alternativas conocidas (o indicar que no se han identificado aún), presupuesto disponible si aplica, modelo de licenciamiento propuesto, tipo de datos que la herramienta tocará
- Autonomía permitida: A1 — Proponer (ficha de evaluación con recomendación de adoptar/rechazar/evaluar más); nunca A2/A3 — este prompt no aprueba presupuesto ni contrata al proveedor
- Detente si: detener y escalar si no hay ningún precio de licencia verificable disponible — no fabricar cifras plausibles; detener si no se identificó ninguna alternativa (incluida la opción de no adoptar) para comparar
- Siguiente: `11-08-finops-cloud-cost-audit` (skill `sdlc-operaciones`)

### 17.4 — Reporte de capacidad y carga del equipo de ingeniería
- Archivo: [references/17-04-reporte-capacidad-equipo.md](references/17-04-reporte-capacidad-equipo.md)
- Cuándo usarlo: al planificar un sprint, quarter o release con compromisos de fecha, o cuando hay señales de sobrecarga del equipo (retrasos recurrentes, burnout, dependencia crítica de una sola persona).
- Entradas: composición actual del equipo (roles, seniority, especialidades, % de disponibilidad semanal), ausencias planeadas por persona y periodo (vacaciones, licencias, capacitación), backlog o roadmap comprometido con estimaciones de esfuerzo por ítem, periodo a eva…
- Autonomía permitida: A0 — Analizar (lectura de composición del equipo, ausencias y backlog comprometido); A1 — Proponer (recomendaciones de redistribución, replanificación o contratación); nunca A2/A3 — este prompt no reasigna tareas ni ejecuta decisiones de personal, eso queda delegado a decisión humana del lead o manager responsable
- Detente si: detener y escalar si no hay backlog/roadmap comprometido con estimaciones de esfuerzo — no inventar estimaciones plausibles; detener si la composición del equipo o las ausencias planeadas no están confirmadas y señalarlo como riesgo residual en vez de asumir disponibilidad completa
- Siguiente: `11-10-capacity-planning` (skill `sdlc-operaciones`), `05-01-plan-implementacion` (skill `sdlc-planificacion`)

### 17.5 — Auditoría de renovación de vendors y contratos tecnológicos
- Archivo: [references/17-05-auditoria-renovacion-vendors.md](references/17-05-auditoria-renovacion-vendors.md)
- Cuándo usarlo: en el ciclo previo a la fecha de renovación de cualquier contrato de vendor tecnológico, SaaS o licencia (idealmente con suficiente antelación para dejar margen de negociación o migración antes del vencimiento).
- Entradas: contrato o términos de licencia vigentes (costo, volumen/asientos contratados, fecha de renovación, cláusulas de cancelación o penalización), datos reales de uso (asientos activos, volumen consumido, frecuencia de uso por equipo/feature), alternativas de merc…
- Autonomía permitida: A0 — Analizar (uso real vs. contratado, comparación de alternativas); A1 — Proponer (recomendación de renovar/renegociar/migrar/cancelar); nunca A2/A3 — este prompt no renueva, cancela, firma ni negocia contratos, ni ejecuta la migración a una alternativa
- Detente si: detener y escalar si no hay datos reales de uso disponibles para calcular la relación uso vs.
- Siguiente: `17-03-evaluacion-herramienta-licencia`

### 17.6 — Reporte de estado a stakeholders
- Archivo: [references/17-06-reporte-estado-stakeholders.md](references/17-06-reporte-estado-stakeholders.md)
- Cuándo usarlo: al cierre de un sprint o hito, o en la cadencia periódica de comunicación acordada con los stakeholders (semanal/quincenal).
- Entradas: hitos comprometidos (de `00-D-01` o el roadmap vigente), issues/PRs cerrados y abiertos en el periodo, estado de CI/CD del periodo, riesgos activos (de `05-02` o el registro vigente), periodo a reportar, audiencia (nivel de detalle técnico esperado)
- Autonomía permitida: A0 — Analizar (recopilar avance real de las fuentes); A1 — Proponer (redacción del reporte en lenguaje de negocio); nunca A2/A3 — este prompt no comunica directamente a los stakeholders, produce el documento para que un humano lo revise y envíe
- Detente si: detener y señalar explícitamente si un hito reportado como "en progreso" no tiene ningún issue/PR asociado verificable — no reportar avance que no pueda trazarse a una fuente real; detener si el periodo a reportar no está definido
- Siguiente: `05-02-riesgos-implementacion` (skill `sdlc-planificacion`), `17-04-reporte-capacidad-equipo`

### 17.7 — Revisión de éxito post-lanzamiento: realización de beneficios contra el Project Charter
- Archivo: [references/17-07-revision-exito-post-lanzamiento.md](references/17-07-revision-exito-post-lanzamiento.md)
- Cuándo usarlo: semanas o meses después del lanzamiento, cuando ya hay datos reales de uso o de negocio disponibles — como cierre formal de un proyecto o como revisión periódica de iniciativas ya lanzadas.
- Entradas: Project Charter original con objetivos/KPIs declarados (`00-D-01`), datos reales de uso/adopción/negocio desde el lanzamiento, ventana de tiempo transcurrida
- Autonomía permitida: A0 — Analizar
- Detente si: si un KPI del Charter no puede medirse con los datos disponibles, no inventes un valor aproximado — repórtalo como "no medible" y señala qué instrumentación faltaría para poder medirlo la próxima vez
- Siguiente: `11-03-deuda-tecnica` (skill `sdlc-operaciones`)

### 17.8 — Retrospectiva de equipo por sprint/iteración
- Archivo: [references/17-08-retrospectiva-equipo-sprint.md](references/17-08-retrospectiva-equipo-sprint.md)
- Cuándo usarlo: al cierre de cada sprint o iteración, como insumo estructurado para (o registro posterior de) la reunión de retrospectiva del equipo.
- Entradas: qué pasó en el sprint/iteración actual (según lo reportado por el equipo, no inferido), retrospectiva(s) anterior(es) con sus acciones de mejora pendientes, si existen
- Autonomía permitida: A0 — Analizar; A1 — Proponer (acciones de mejora priorizadas)
- Detente si: no inventar problemas, logros o causas raíz que el equipo no reportó explícitamente — si algo no fue mencionado por el equipo, no se incluye como si lo hubiera sido; si una acción de mejora de la retrospectiva anterior nunca se completó, reportarlo explícitamente en vez de omitirlo
- Siguiente: `11-03-deuda-tecnica` (skill `sdlc-operaciones`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
