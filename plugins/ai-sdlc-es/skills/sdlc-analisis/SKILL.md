---
name: sdlc-analisis
description: "Prompts AI-SDLC de análisis de requerimientos e issues. Úsala cuando pidan analizar un issue, requerimiento o cambio: alcance funcional, análisis técnico, impacto cruzado, elicitación con interesados, requerimientos no funcionales, triage del backlog de GitHub o matriz de trazabilidad."
license: CC-BY-4.0
---

# Fase AI-SDLC 02 — Análisis de requerimientos e issues

Esta skill agrupa los prompts de la fase **Análisis de requerimientos e issues** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 2.0 — Elicitación de requerimientos con stakeholders
- Archivo: [references/02-00-elicitacion-requerimientos-stakeholders.md](references/02-00-elicitacion-requerimientos-stakeholders.md)
- Cuándo usarlo: al inicio de una iniciativa nueva, cuando solo existe una idea vaga o una queja de negocio, antes de que exista un issue o requerimiento redactado formalmente.
- Entradas: contexto de la iniciativa (idea, queja o necesidad inicial en bruto), rol(es) de stakeholder a entrevistar, transcripción o notas de la conversación si ya ocurrió (o "sesión aún no realizada" si se pide el guion antes), objetivo de negocio de la iniciativa (o…
- Autonomía permitida: A0 — Analizar (síntesis de una conversación ya ocurrida); A1 — Proponer (guion de entrevista, preguntas de sondeo)
- Detente si: si la transcripción o notas no permiten distinguir una necesidad real de una solución ya asumida por el stakeholder, señalarlo explícitamente en vez de aceptar la solución propuesta como el requerimiento; si falta el rol del stakeholder u otro dato necesario para el guion, solicitarlo antes de gene…
- Siguiente: `02-05-analisis-integral-requerimientos`, `02-01-analisis-issue`

### 2.1 — Análisis funcional de un requerimiento, issue o cambio
- Archivo: [references/02-01-analisis-issue.md](references/02-01-analisis-issue.md)
- Cuándo usarlo: como primer paso al recibir una tarea, antes de cualquier análisis técnico o diseño.
- Entradas: issue o requerimiento a analizar, repositorio, módulo o funcionalidad, workspace/subproyecto y estándar/compliance aplicable
- Autonomía permitida: A0 — Analizar
- Detente si: si el issue no aporta información suficiente para fijar comportamiento esperado o criterios de aceptación, declarar el vacío y bajar el `confidence_score` en vez de inventar el alcance
- Siguiente: `02-02-analisis-tecnico`

### 2.2 - Análisis técnico profundo de código existente
- Archivo: [references/02-02-analisis-tecnico.md](references/02-02-analisis-tecnico.md)
- Cuándo usarlo: después del análisis funcional (`02-01`) y antes del análisis de impacto cruzado (`02-03`) y del diseño de la solución (`04-01`).
- Entradas: resultado de `02-01`, repositorio o workspace, issue o requerimiento, rama o commit objetivo, ambiente, documentos y contratos a revisar
- Autonomía permitida: A0 — Analizar
- Detente si: si el comportamiento no puede verificarse en runtime, declararlo como análisis estático; si el `status` del JSON de metadatos resulta `blocked`, detener y escalar en vez de forzar conclusiones
- Siguiente: `02-03-impacto-cruzado`

### 2.3 — Análisis de impacto cruzado
- Archivo: [references/02-03-impacto-cruzado.md](references/02-03-impacto-cruzado.md)
- Cuándo usarlo: después del análisis técnico profundo (`02-02`) y antes del diseño de la solución (`04-01`).
- Entradas: resultado de `02-02` (flujo técnico y dependencias), arquitectura, contratos de API, esquema de base de datos, componentes involucrados
- Autonomía permitida: A0 — Analizar
- Detente si: si no hay evidencia suficiente para descartar impacto en un componente crítico (seguridad, datos, producción, semver), clasificarlo como riesgo alto no confirmado en vez de omitirlo de la matriz
- Siguiente: `04-01-diseno-solucion` (skill `sdlc-diseno`)

### 2.4 — Triage y planificación de backlog de GitHub Issues
- Archivo: [references/02-04-triage-backlog-github.md](references/02-04-triage-backlog-github.md)
- Cuándo usarlo: cuando se necesita revisar issues abiertos o pendientes como cartera de trabajo, ordenar su atención por prioridad o componente, o preparar un plan maestro de ejecución para un sprint, remediación o estabilización.
- Entradas: fuente de issues (por ejemplo, salida JSON de `gh issue list`), filtro aplicado, criterio de backlog pendiente, componente o responsable objetivo, rama y ambiente objetivo, documentos a revisar
- Autonomía permitida: A1 — Proponer
- Detente si: no proponer cierre de issues sin evidencia; si la información de un issue no basta para clasificarlo con precisión, declararlo como supuesto y reducir el nivel de confianza en vez de asignarle prioridad definitiva
- Siguiente: `05-01-plan-implementacion` (skill `sdlc-planificacion`), `02-01-analisis-issue`

### 2.5 — Análisis Integral de Requerimientos y Generación de Issues (PRO)
- Archivo: [references/02-05-analisis-integral-requerimientos.md](references/02-05-analisis-integral-requerimientos.md)
- Cuándo usarlo: al recibir un requerimiento de usuario complejo, una solicitud de cambio (CR) o una idea de producto que aún no ha sido formalizada técnicamente.
- Entradas: requerimiento_usuario (idea o CR sin formalizar), repositorio, rama_base, documentación y código relacionado existentes
- Autonomía permitida: A1 — Proponer
- Detente si: si no puede confirmarse el cumplimiento de la Definition of Ready (criterios de aceptación, alcance o impacto verificable), marcar el issue resultante como "no listo" en vez de presentarlo como Ready
- Siguiente: `02-04-triage-backlog-github`, `04-01-diseno-solucion` (skill `sdlc-diseno`), `02-07-matriz-trazabilidad-requerimientos`

### 2.6 — Especificación de requerimientos no funcionales
- Archivo: [references/02-06-requerimientos-no-funcionales.md](references/02-06-requerimientos-no-funcionales.md)
- Cuándo usarlo: después de tener los requerimientos funcionales definidos (`02-05`) o la arquitectura tentativa (`00-D-02`), y antes del diseño de solución (`04-01`) — los RNF condicionan decisiones de diseño que son costosas de revertir si se descubren tarde.
- Entradas: contexto del sistema o cambio, requerimientos funcionales ya definidos (de `02-05`/`04-03`) si existen, restricciones de negocio conocidas (SLA contractual, compliance, presupuesto de infraestructura), arquitectura o stack tentativo si existe (`00-D-02`)
- Autonomía permitida: A0 — Analizar (catalogar RNF ya declarados o inferibles del contexto); A1 — Proponer (umbrales sugeridos cuando el negocio no los ha fijado, siempre marcados explícitamente como propuesta a validar)
- Detente si: si un RNF no puede expresarse con un umbral medible (número, unidad, condición de prueba), no lo declares como definido — regístralo como "pendiente de cuantificar" en vez de inventar una cifra
- Siguiente: `04-01-diseno-solucion` (skill `sdlc-diseno`), `07-06-pruebas-performance-carga` (skill `sdlc-pruebas`)

### 2.7 — Matriz de trazabilidad de requerimientos del proyecto completo
- Archivo: [references/02-07-matriz-trazabilidad-requerimientos.md](references/02-07-matriz-trazabilidad-requerimientos.md)
- Cuándo usarlo: periódicamente durante la ejecución de un proyecto con múltiples requerimientos ya analizados (`02-05`), para detectar requerimientos huérfanos (sin diseño, código o prueba) o código sin requerimiento formal que lo respalde, antes de que el proyecto se dé por cerrado.
- Entradas: lista de requerimientos de negocio del proyecto (o issues ya analizados con `02-05`), diseños asociados, PRs/implementaciones relacionadas, resultados de prueba disponibles
- Autonomía permitida: A0 — Analizar (agregar trazabilidad ya evidenciable); A1 — Proponer (marcar huecos y priorizarlos)
- Detente si: si un requerimiento no puede vincularse a ninguna evidencia de diseño, código o prueba, no lo marques como "cubierto" — repórtalo explícitamente como huérfano
- Siguiente: `08-01-revision-completa-pr` (skill `sdlc-revision`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
