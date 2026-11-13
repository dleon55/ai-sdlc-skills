---
name: sdlc-incidentes
description: "Prompts AI-SDLC de incidentes y causa raíz. Úsala cuando haya un bug, falla o incidente reportado en GitHub y se necesite investigarlo: reproducción, evidencia, análisis de causa raíz (RCA) y propuesta de corrección."
license: CC-BY-4.0
---

# Fase AI-SDLC 03 — Incidentes y causa raíz

Esta skill agrupa los prompts de la fase **Incidentes y causa raíz** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 3.1 — Revisión de incidentes reportados por tester contra GitHub Issues
- Archivo: [references/03-01-incidentes-github.md](references/03-01-incidentes-github.md)
- Cuándo usarlo: al recibir un reporte de ciclo de QA, antes de gestionar cualquier defecto en GitHub.
- Entradas: reporte de incidentes de QA normalizado, acceso de lectura a issues abiertos y cerrados en GitHub
- Autonomía permitida: A1 — Proponer (redacta issues y acciones, no las ejecuta)
- Detente si: el propio prompt restringe explícitamente su alcance a análisis y redacción; nunca ejecutar acciones de mutación en GitHub
- Siguiente: `03-02-causa-raiz`

### 3.2 — Análisis de causa raíz
- Archivo: [references/03-02-causa-raiz.md](references/03-02-causa-raiz.md)
- Cuándo usarlo: al investigar defectos en QA o producción, cuando el síntoma está claro pero la causa no.
- Entradas: logs, código, configuraciones, commits y despliegues recientes; issue o incidente de referencia
- Autonomía permitida: A0 — Analizar
- Detente si: si no se puede confirmar la causa raíz, declarar nivel de confianza y evidencia faltante en vez de forzar una conclusión
- Siguiente: `05-01-plan-implementacion` (skill `sdlc-planificacion`), `08-03-remediacion-maestro` (skill `sdlc-revision`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
