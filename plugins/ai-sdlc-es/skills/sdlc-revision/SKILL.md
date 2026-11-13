---
name: sdlc-revision
description: "Prompts AI-SDLC de revisión de código y pr. Úsala cuando pidan revisar un pull request completo, un plan de remediación de hallazgos, perfilar consultas SQL o revisar una migración de esquema de base de datos."
license: CC-BY-4.0
---

# Fase AI-SDLC 08 — Revisión de código y PR

Esta skill agrupa los prompts de la fase **Revisión de código y PR** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 8.1 — Revisión completa de PR: calidad, cumplimiento e integración
- Archivo: [references/08-01-revision-completa-pr.md](references/08-01-revision-completa-pr.md)
- Cuándo usarlo: después de implementar cambios y antes de mergear cualquier PR — es el paso de revisión completo previo a merge, en un solo prompt en vez de varias invocaciones separadas.
- Entradas: diff real del PR, issue/requerimiento asociado, diseño aprobado si existe, resultados de pruebas, historial de commits y ramas activas relacionadas, logs de CI local y de GitHub Actions, estándares de código del proyecto
- Autonomía permitida: A1 — Proponer (el veredicto y la estrategia de integración quedan propuestos; ejecutar el merge, aplicar remediación o resolver conflictos requiere un prompt de ejecución separado y aprobación humana)
- Detente si: si falta el diff completo, el requerimiento original, o alguno de los cuatro insumos de cumplimiento (solicitado/diseñado/implementado/probado), declara la brecha de evidencia en esa dimensión específica en vez de omitirla o asumir que está en orden; si el estado local no está sincronizado con el r…
- Siguiente: `08-03-remediacion-maestro`, `09-04-promotion-checklist` (skill `sdlc-integracion`)

### 8.3 — Remediación de revisión estática (prompt maestro)
- Archivo: [references/08-03-remediacion-maestro.md](references/08-03-remediacion-maestro.md)
- Cuándo usarlo: cuando se recibe un reporte de revisión estática y se necesita un plan estructurado de corrección, no solo parches superficiales.
- Entradas: reporte de revisión estática con hallazgos críticos, medios y menores
- Autonomía permitida: A1 — Proponer (bloque 1); A2 — Ejecutar controlado (bloque 2, solo tras aprobación humana del plan del bloque 1)
- Detente si: no iniciar el bloque de ejecución sin aprobación explícita del plan de análisis; detener si un cambio propuesto afecta la estabilidad del sistema sin mitigación clara
- Siguiente: `07-01-pruebas-unitarias` (skill `sdlc-pruebas`), `07-02-pruebas-integracion` (skill `sdlc-pruebas`)

### 8.4 — Auditoría de Planes de Ejecución y Profiling SQL (DBA)
- Archivo: [references/08-04-sql-query-profiling.md](references/08-04-sql-query-profiling.md)
- Cuándo usarlo: Cuando un endpoint o servicio presenta lentitud (latencia alta) en producción, o durante la revisión de PRs que introducen consultas complejas a la base de datos.
- Entradas: `EXPLAIN ANALYZE` o log del ORM, DDL o modelos del esquema relevante, motor de base de datos usado
- Autonomía permitida: A1 — Proponer (entrega diagnóstico, query optimizada y DDL de índices como propuesta; no los ejecuta)
- Detente si: si el esquema o el plan de ejecución no incluye volumetría real ni estadísticas actualizadas de las tablas, presentar el diagnóstico como preliminar y no garantizar el impacto estimado
- Siguiente: `08-01-revision-completa-pr`

### 8.5 — Revisión de migración de esquema de base de datos
- Archivo: [references/08-05-revision-migracion-esquema-bd.md](references/08-05-revision-migracion-esquema-bd.md)
- Cuándo usarlo: antes de ejecutar una migración de esquema contra staging o producción — como parte del PR que introduce el archivo de migración, o como último control antes del `migrate up` en el pipeline de despliegue.
- Entradas: script o archivo de migración (DDL exacto, up y down si existen), motor de base de datos y versión, tamaño aproximado y tráfico de la(s) tabla(s) afectada(s), fragmento relevante del código actualmente desplegado que lee o escribe esas columnas/tablas, estrat…
- Autonomía permitida: A0 — Analizar (diagnóstico de riesgo); A1 — Proponer (versión corregida de la migración, plan expand-contract, script de rollback, como propuesta); nunca A2/A3 — este prompt no ejecuta ni aplica la migración bajo ninguna circunstancia
- Detente si: detener y escalar a aprobación humana explícita si la migración toma un lock de tabla completo sobre una tabla de alto tráfico sin plan de ventana de mantenimiento; detener si no se puede confirmar compatibilidad con el código actualmente desplegado; nunca dar por aceptable una operación con pérdid…
- Siguiente: `11-09-runbook-rollback` (skill `sdlc-operaciones`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
