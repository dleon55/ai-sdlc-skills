---
name: sdlc-planificacion
description: "Prompts AI-SDLC de planificación de la implementación. Úsala cuando haya que convertir un diseño aprobado en un plan de implementación por pasos o evaluar los riesgos de implementarlo."
license: CC-BY-4.0
---

# Fase AI-SDLC 05 — Planificación de la implementación

Esta skill agrupa los prompts de la fase **Planificación de la implementación** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 5.1 — Plan de implementación detallado
- Archivo: [references/05-01-plan-implementacion.md](references/05-01-plan-implementacion.md)
- Cuándo usarlo: después del diseño aprobado (`04-01`), antes de ejecutar cualquier cambio en el repositorio.
- Entradas: diseño aprobado (`04-01`), arquitectura, contratos, rama objetivo, ambiente de destino, componentes a modificar
- Autonomía permitida: A1 — Proponer (plan o artefacto sin aplicar); no autoriza por sí sola ejecutar, commitear ni desplegar
- Detente si: detener si no existe diseño aprobado del cual partir; no dejar pasos sin evidencia esperada, dependencia o riesgo declarado; señalar explícitamente si algún paso requiere ambiente de producción
- Siguiente: `05-02-riesgos-implementacion`, `06-01-implementacion-multiagente` (skill `sdlc-implementacion`), `07-00-deteccion-stack-pruebas` (skill `sdlc-pruebas`)

### 5.2 — Análisis de riesgos e impacto de implementación
- Archivo: [references/05-02-riesgos-implementacion.md](references/05-02-riesgos-implementacion.md)
- Cuándo usarlo: en paralelo al plan de implementación (`05-01`), antes de ejecutar cualquier cambio.
- Entradas: diseño aprobado, arquitectura, historial de incidentes, plan de implementación (`05-01`) en curso o aprobado
- Autonomía permitida: A0 — Analizar riesgos e impacto potencial; A1 — Proponer la matriz de riesgos con mitigación y contingencia
- Detente si: detener si no hay diseño o plan de referencia; escalar a revisión humana antes de continuar a `06-01` si algún riesgo queda clasificado como alto sin mitigación viable
- Siguiente: `06-01-implementacion-multiagente` (skill `sdlc-implementacion`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
