---
name: sdlc-negocio-qa
description: "Prompts AI-SDLC de negocio y qa funcional. Úsala cuando haya que redactar historias de usuario con Gherkin, casos de prueba manuales o analizar defectos desde el punto de vista del negocio."
license: CC-BY-4.0
---

# Fase AI-SDLC 15 — Negocio y QA funcional

Esta skill agrupa los prompts de la fase **Negocio y QA funcional** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 15.1 — Historias de usuario y criterios de aceptación Gherkin
- Archivo: [references/15-01-historias-usuario-gherkin.md](references/15-01-historias-usuario-gherkin.md)
- Cuándo usarlo: al definir requerimientos de negocio detallados, antes del diseño técnico o arquitectura.
- Entradas: requerimiento o solicitud de negocio a convertir, módulo o proceso afectado, estándar de compliance aplicable si existe (ISO 29110 / MOPROSOFT)
- Autonomía permitida: A1 — Proponer las historias de usuario y criterios de aceptación como artefacto de documentación
- Detente si: no inventar reglas de negocio, roles o flujos que no estén implícitos en la solicitud original; si el requerimiento es ambiguo, señalar los supuestos usados en vez de asumir silenciosamente
- Siguiente: `04-01-diseno-solucion` (skill `sdlc-diseno`), `15-02-casos-prueba-manuales`

### 15.2 — Diseño de casos de prueba manuales y funcionales
- Archivo: [references/15-02-casos-prueba-manuales.md](references/15-02-casos-prueba-manuales.md)
- Cuándo usarlo: al planificar la fase de pruebas de una funcionalidad, antes de iniciar pruebas exploratorias o manuales.
- Entradas: historia de usuario o requerimiento a validar, criterios de aceptación o reglas de negocio si existen (idealmente de `15-01`)
- Autonomía permitida: A1 — Proponer la suite de casos de prueba manuales como artefacto listo para ejecución por QA
- Detente si: no inventar reglas de negocio o comportamientos del sistema no descritos en el requerimiento; si faltan criterios de aceptación, señalarlo y limitar la cobertura a lo verificable con la información disponible
- Siguiente: `07-05-automatizacion-antigravity` (skill `sdlc-pruebas`), `07-03-pruebas-e2e` (skill `sdlc-pruebas`)

### 15.3 — Reporte y análisis de defectos con impacto en negocio
- Archivo: [references/15-03-analisis-defectos-negocio.md](references/15-03-analisis-defectos-negocio.md)
- Cuándo usarlo: al reportar un fallo en el backlog de incidentes, asegurando que contenga toda la información necesaria para el desarrollador.
- Entradas: descripción del error observado, pasos realizados, comportamiento esperado, evidencia técnica si existe (log, código HTTP, captura)
- Autonomía permitida: A1 — Proponer
- Detente si: si la severidad técnica y la prioridad de negocio no pueden justificarse con la evidencia dada, declararlo en vez de asumir un nivel de impacto
- Siguiente: `03-01-incidentes-github` (skill `sdlc-incidentes`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
