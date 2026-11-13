---
name: sdlc-comprension
description: "Prompts AI-SDLC de comprensión del repositorio y de los procesos. Úsala cuando haya que entender un repositorio o sistema existente antes de tocarlo: arranque y mapa del código, módulos, dependencias, flujos y procesos de negocio que implementa."
license: CC-BY-4.0
---

# Fase AI-SDLC 01 — Comprensión del repositorio y de los procesos

Esta skill agrupa los prompts de la fase **Comprensión del repositorio y de los procesos** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 1.1 — Inventario técnico del repositorio
- Archivo: [references/01-01-arranque-comprension-repositorio.md](references/01-01-arranque-comprension-repositorio.md)
- Cuándo usarlo: al arrancar trabajo sobre un repositorio del que no se tiene contexto previo, o para refrescar el inventario después de cambios estructurales significativos.
- Entradas: acceso de lectura al repositorio completo (código fuente, configuración, documentación existente); no requiere issue ni incidente de referencia
- Autonomía permitida: A0 — Analizar
- Detente si: si partes del repositorio no son accesibles o el monorepo tiene workspaces no resueltos, declarar el alcance cubierto y los vacíos en vez de inferir estructura no verificada
- Siguiente: `01-02-analisis-procesos`, `02-01-analisis-issue` (skill `sdlc-analisis`)

### 1.2 — Localizar procesos, procedimientos y políticas del proyecto
- Archivo: [references/01-02-analisis-procesos.md](references/01-02-analisis-procesos.md)
- Cuándo usarlo: antes de cualquier trabajo de análisis o implementación, para entender el marco de gobierno del proyecto y evitar violar reglas ya definidas.
- Entradas: acceso de lectura a README, docs/, wiki exportada, ADRs, archivos de contribución y workflows del repositorio
- Autonomía permitida: A0 — Analizar
- Detente si: si no se encuentra evidencia documental de una categoría de gobierno (por ejemplo, seguridad o branching), declararla como "no existe" en vez de asumir una política implícita
- Siguiente: `01-01-arranque-comprension-repositorio`, `02-01-analisis-issue` (skill `sdlc-analisis`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
