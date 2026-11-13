---
name: sdlc-monorepo-estandares
description: "Prompts AI-SDLC de monorepo y estándares de calidad. Úsala cuando trabajes un monorepo (workspaces y dependencias) o haya que medir calidad y cumplimiento con PSP/TSP, ISO o MoProSoft."
license: CC-BY-4.0
---

# Fase AI-SDLC 14 — Monorepo y estándares de calidad

Esta skill agrupa los prompts de la fase **Monorepo y estándares de calidad** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 14.1 — Auditoría de dependencias y workspaces en monorepos
- Archivo: [references/14-01-monorepo-workspaces-dependencias.md](references/14-01-monorepo-workspaces-dependencias.md)
- Cuándo usarlo: al inicio de un cambio técnico mayor o refactorización que afecte a bibliotecas compartidas (`packages/`, `shared/`) dentro de un monorrepositorio.
- Entradas: workspace/subproyecto origen a analizar, archivos de configuración del monorepo (package.json, pnpm-workspace.yaml, go.work, lerna.json, turbo.json, tsconfig.json)
- Autonomía permitida: A0 — Analizar
- Detente si: si los archivos de configuración del monorepo no son accesibles o son ambiguos, declarar el grafo como incompleto en vez de asumir relaciones de dependencia no verificadas
- Siguiente: `05-01-plan-implementacion` (skill `sdlc-planificacion`), `04-04-adr-decisiones-arquitectura` (skill `sdlc-diseno`)

### 14.2 — Registro de métricas de calidad y estimaciones PSP/TSP
- Archivo: [references/14-02-psp-tsp-metricas-calidad.md](references/14-02-psp-tsp-metricas-calidad.md)
- Cuándo usarlo: al inicio del desarrollo para registrar la estimación base (plan) y al finalizar cada fase de ingeniería de software para registrar el esfuerzo y defectos reales.
- Entradas: issue o requerimiento actual, fase del ciclo (Planeación, Diseño, Codificación, Revisión de Código, Pruebas, Post-mortem), métricas o bitácora previa si existen
- Autonomía permitida: A0 — Analizar el estado actual; A1 — Proponer el registro actualizado de estimaciones y métricas reales
- Detente si: no inventar tiempos reales o defectos no reportados por la persona desarrolladora; si falta la estimación base (plan) de una fase, solicitarla antes de calcular rendimiento o densidad de defectos
- Siguiente: `14-03-iso-moprosoft-compliance`

### 14.3 — Auditoría de cumplimiento de procesos ISO 29110 / MOPROSOFT
- Archivo: [references/14-03-iso-moprosoft-compliance.md](references/14-03-iso-moprosoft-compliance.md)
- Cuándo usarlo: antes del despliegue en entornos controlados (Staging / Prod), como parte de las puertas de calidad (Quality Gates) en la liberación.
- Entradas: workspace/subproyecto y estándar de compliance a auditar (ISO 29110 / MOPROSOFT / MAAGTICSI), artefactos generados (Plan de Implementación, Casos de Prueba, Código de Pruebas, Memoria Técnica), evidencia de seguridad de la información (reporte SAST/DAST o pol…
- Autonomía permitida: A0 — Analizar la conformidad de cada artefacto; A1 — Proponer el veredicto y las acciones de remediación obligatorias
- Detente si: no emitir veredicto "Aprobado" si falta trazabilidad bidireccional requerimiento-diseño-código-pruebas; marcar como "Rechazado" o "Aprobado con Reservas" ante cualquier no conformidad sin evidencia de mitigación
- Siguiente: `08-03-remediacion-maestro` (skill `sdlc-revision`), `09-04-promotion-checklist` (skill `sdlc-integracion`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
