---
name: sdlc-orquestador
description: "Prompts AI-SDLC de orquestador del ciclo completo. Úsala cuando una asignación grande requiera coordinar varias fases, capacidades o agentes y haya que decidir el flujo mínimo suficiente; para una tarea simple usa directamente la skill de su fase."
license: CC-BY-4.0
---

# Fase AI-SDLC 12 — Orquestador del ciclo completo

Esta skill agrupa los prompts de la fase **Orquestador del ciclo completo** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 12 — Prompt maestro orquestador del ciclo completo
- Archivo: [references/12-orquestador.md](references/12-orquestador.md)
- Cuándo usarlo: cuando una asignación requiere coordinación entre varias capacidades, fases o agentes. Para tareas simples, utiliza directamente el prompt especializado correspondiente.
- Entradas: issue/requerimiento, rama objetivo, ambiente, componentes, nivel de autonomía permitido, herramientas disponibles, presupuesto
- Autonomía permitida: definida dinámicamente por el propio prompt (Paso 3, "Crear contrato"); nunca debe exceder el nivel de autonomía de entrada declarado ni el techo de autonomía propio del prompt destino de la delegación — se otorga el mínimo de ambos
- Detente si: "No ejecutes todas las fases por defecto"; escalar a humano cuando el riesgo o permiso exceda el contrato generado, o cuando la autonomía de entrada supere el techo de autonomía propio del prompt destino de una delegación

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
