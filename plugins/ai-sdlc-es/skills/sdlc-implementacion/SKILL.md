---
name: sdlc-implementacion
description: "Prompts AI-SDLC de implementación y commits. Úsala cuando toque implementar cambios con uno o varios agentes de IA, coordinar un programa multiagente o preparar commits limpios y convencionales."
license: CC-BY-4.0
---

# Fase AI-SDLC 06 — Implementación y commits

Esta skill agrupa los prompts de la fase **Implementación y commits** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 6.1 — Implementación multi-agente segura
- Archivo: [references/06-01-implementacion-multiagente.md](references/06-01-implementacion-multiagente.md)
- Cuándo usarlo: durante la fase de ejecución, después de que el plan (`05-01`) y los riesgos (`05-02`) han sido aprobados.
- Entradas: plan de implementación aprobado (`05-01`), matriz de riesgos aprobada (`05-02`), diseño técnico, rama/worktree aislado disponible, presupuesto explícito de archivos, tiempo e intentos
- Autonomía permitida: A2 — Ejecutar controlado (editar y validar en workspace o rama aislada); nunca A3 (commit/push/PR/despliegue) sin autorización explícita adicional
- Detente si: detener de inmediato si se agota el presupuesto de archivos, tiempo o intentos antes de completar el alcance, entregando el estado parcial; detener ante drift o conflicto textual/contractual/semántico que no pueda resolverse preservando el trabajo existente; no modificar archivos fuera del alcance…
- Siguiente: `06-02-commits`

### 6.2 — Generación de mensajes de commit de calidad
- Archivo: [references/06-02-commits.md](references/06-02-commits.md)
- Cuándo usarlo: antes de hacer commit de cualquier cambio, para garantizar trazabilidad y consistencia con el historial del repositorio.
- Entradas: issue, tipo de cambio, componente, descripción breve del cambio ya realizado
- Autonomía permitida: A1 — Proponer (el commit/push real lo ejecuta el flujo estándar de git, no este prompt)
- Detente si: si el cambio descrito mezcla intenciones no relacionadas, detener y recomendar dividir en commits separados antes de proponer el mensaje final
- Siguiente: `08-01-revision-completa-pr` (skill `sdlc-revision`)

### 6.3 — Coordinación de programa multiagente
- Archivo: [references/06-03-coordinacion-programa-multiagente.md](references/06-03-coordinacion-programa-multiagente.md)
- Cuándo usarlo: cuando varios agentes IA (u otros colaboradores) trabajan simultáneamente sobre distintos módulos de un mismo programa de desarrollo o mantenimiento y se necesita un plan de trabajo centralizado, trazable y verificable en cada iteración.
- Entradas: estado real del repositorio (issues abiertos, PRs, branches activas, resultado de CI), plan de trabajo previo si existe, lista de agentes disponibles y su especialidad, criterios de aceptación del programa
- Autonomía permitida: A1 — Proponer (plan, asignaciones, prompts por agente y veredictos de revisión quedan propuestos; la ejecución la realiza cada agente bajo su propio contrato de autonomía, y el merge/despliegue requiere aprobación humana)
- Detente si: si el estado real del repositorio no puede confirmarse (issues/PRs/CI inaccesibles), declarar el plan como desactualizado en vez de asumir avance; si dos agentes reclaman ownership del mismo archivo/módulo sin resolución, detener la asignación y escalar el conflicto antes de continuar
- Siguiente: `06-01-implementacion-multiagente`, `12-orquestador` (skill `sdlc-orquestador`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
