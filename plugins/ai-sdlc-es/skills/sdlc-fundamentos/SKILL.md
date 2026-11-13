---
name: sdlc-fundamentos
description: "Prompts AI-SDLC de fundamentos del proyecto y gobernanza de agentes. Úsala al arrancar un proyecto o un repositorio nuevo: acta (project charter), caso de negocio, stack y arquitectura inicial, plan de trabajo, registro de riesgos, estructura del repositorio, configuración de GitHub, gobernanza de agentes de IA, metodología, calidad de código, o redactar un issue y un plan para que lo ejecute un agente."
license: CC-BY-4.0
---

# Fase AI-SDLC 00 — Fundamentos del proyecto y gobernanza de agentes

Esta skill agrupa los prompts de la fase **Fundamentos del proyecto y gobernanza de agentes** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 0-B.1 — Scaffolding de repositorio nuevo
- Archivo: [references/00-B-01-scaffolding-repositorio.md](references/00-B-01-scaffolding-repositorio.md)
- Cuándo usarlo: al iniciar un proyecto nuevo, al migrar un proyecto sin estructura formal, o al estandarizar un repositorio existente que creció sin guía.
- Entradas: tipo de proyecto, metodología, stack tecnológico, plataforma de hosting/CI, composición del equipo, tipo de licencia
- Autonomía permitida: A1 — Proponer
- Detente si: si el tipo de proyecto o el stack son ambiguos, o si ya existe una estructura en conflicto con la propuesta, declarar la ambigüedad y pedir confirmación antes de proponer una reestructuración completa
- Siguiente: `00-B-03-github-configuracion`, `00-B-05-stack-calidad-codigo`, `00-B-02-gobernanza-ia-agentes`, `00-B-04-metodologia-framework`

### 0-B.2 — Configuración de archivos de gobernanza para agentes IA
- Archivo: [references/00-B-02-gobernanza-ia-agentes.md](references/00-B-02-gobernanza-ia-agentes.md)
- Cuándo usarlo: al iniciar un repositorio nuevo, al incorporar agentes IA a un proyecto existente, o cuando los agentes no siguen las convenciones ni el marco de trabajo del proyecto.
- Entradas: nombre y stack del proyecto, metodología, plataformas de agentes IA activas, nivel de autonomía permitido, reglas críticas y patrones prohibidos del proyecto, herramientas/integraciones disponibles, clasificación de datos y ambientes
- Autonomía permitida: A1 — Proponer
- Detente si: si no se puede confirmar qué agentes están realmente activos en el repositorio, no generar configuración para agentes hipotéticos; si las reglas críticas declaradas se contradicen entre sí, señalar el conflicto en vez de resolverlo arbitrariamente
- Siguiente: `00-C-03-configuracion-por-agente`

### 0-B.3 — Configuración de repositorio GitHub (protecciones, plantillas y settings)
- Archivo: [references/00-B-03-github-configuracion.md](references/00-B-03-github-configuracion.md)
- Cuándo usarlo: al crear un repositorio nuevo, al estandarizar uno existente, o cuando el repo no tiene protecciones formales y se va a incorporar IA o múltiples contribuidores.
- Entradas: organización/usuario y nombre del repositorio, metodología de branching, ramas a proteger, composición del equipo, ambientes de despliegue, stack de CI
- Autonomía permitida: A1 — Proponer
- Detente si: si no se conoce con certeza el estado actual de branch protection, los roles del equipo o los ambientes reales, declarar el supuesto explícitamente en vez de generar reglas que podrían bloquear al equipo real al aplicarse
- Siguiente: `00-B-05-stack-calidad-codigo`

### 0-B.4 — Selección y configuración de metodología y marco de trabajo
- Archivo: [references/00-B-04-metodologia-framework.md](references/00-B-04-metodologia-framework.md)
- Cuándo usarlo: al iniciar un proyecto, al formalizar uno existente que creció sin metodología, o cuando se incorporan agentes IA y se necesita definir su lugar en el proceso.
- Entradas: tipo de proyecto, tamaño del equipo (personas + tipos de agentes IA), frecuencia de entregas esperada, metodología candidata o elegida, integraciones/dependencias de terceros, nivel de madurez actual del equipo
- Autonomía permitida: A1 — Proponer
- Detente si: si la metodología candidata requiere condiciones que el equipo declarado no cumple (ej. SCRUM completo con equipo de una persona), señalar la alerta explícitamente en vez de recomendarla sin reservas
- Siguiente: `00-B-01-scaffolding-repositorio`, `00-B-03-github-configuracion`, `17-08-retrospectiva-equipo-sprint` (skill `sdlc-backoffice-ingenieria`)

### 0-B.5 — Configuración de stack y herramientas de calidad de código
- Archivo: [references/00-B-05-stack-calidad-codigo.md](references/00-B-05-stack-calidad-codigo.md)
- Cuándo usarlo: al iniciar un proyecto, al estandarizar calidad en uno existente, o cuando se incorporan agentes IA que deben respetar las convenciones del stack.
- Entradas: lenguaje(s) y framework(s) principales, plataforma de CI, cobertura mínima deseada, nivel de restricción (permisivo/balanceado/estricto)
- Autonomía permitida: A1 — Proponer
- Detente si: si el stack detectado es ambiguo o mixto sin un lenguaje principal claro, pedir confirmación antes de generar una configuración exhaustiva que podría no aplicar
- Siguiente: `00-B-03-github-configuracion`

### 0-C.1 — Documentar un issue listo para ejecución por agente IA
- Archivo: [references/00-C-01-issue-para-agente-ia.md](references/00-C-01-issue-para-agente-ia.md)
- Cuándo usarlo: antes de asignar cualquier tarea a un agente IA (Copilot Agent, Claude, Codex, Windsurf), para garantizar que el agente opere con contexto completo y dentro de límites seguros.
- Entradas: título y tipo del issue, descripción del problema/requerimiento, repositorio y rama destino, ambiente, archivos/módulos involucrados (si se conocen), criterios de aceptación, restricciones, agente asignado, resultado observable esperado, permisos/herramientas…
- Autonomía permitida: A1 — Proponer (redacta el issue y el comando sugerido; publicarlo en GitHub es una acción A3 que queda fuera de este prompt)
- Detente si: si la información disponible no permite completar el `## Contrato de ejecución` (modo de autonomía, herramientas, alcance) de forma no ambigua, declarar el issue como "NO apto para agente" en la evaluación de readiness en vez de rellenar valores inventados
- Siguiente: `00-C-02-plan-mode-multiagente`

### 0-C.2 — Modo plan seguro y coordinación multi-agente
- Archivo: [references/00-C-02-plan-mode-multiagente.md](references/00-C-02-plan-mode-multiagente.md)
- Cuándo usarlo: siempre antes de ejecutar tareas de alto impacto, cuando hay más de un agente activo en el repo, o cuando se trabaja en `mode:plan` en Agent Manager o GitHub Copilot Agent.
- Entradas: issue/tarea de referencia, rama objetivo, agentes activos en paralelo si se conocen; estado local del repositorio (rama, worktrees, commits recientes, PRs abiertos)
- Autonomía permitida: A1 — Proponer
- Detente si: si el Paso 2 (detección de conflictos) encuentra un conflicto potencial o activo — mismo archivo tocado por otro agente o PR abierto — DETENER de inmediato y reportar antes de continuar; no pasar a ejecución controlada sin confirmación humana
- Siguiente: `06-01-implementacion-multiagente` (skill `sdlc-implementacion`)

### 0-C.3 — Configuración específica por tipo de agente IA
- Archivo: [references/00-C-03-configuracion-por-agente.md](references/00-C-03-configuracion-por-agente.md)
- Cuándo usarlo: al incorporar un nuevo tipo de agente al proyecto, al detectar que un agente no sigue las convenciones, o al configurar un entorno multi-agente por primera vez. Requiere que la gobernanza base ya exista (ver `00-B-02-gobernanza-ia-agentes`); este prompt configura mecanismos específicos por agente, no la base.
- Entradas: lista de agentes activos (Copilot, Claude vía chat/API, Claude Code, Codex, Windsurf, Cursor, Antigravity), stack del proyecto, metodología, reglas críticas del proyecto, nivel de autonomía general; gobernanza base ya existente (`00-B-02`)
- Autonomía permitida: A1 — Proponer
- Detente si: si se solicita configurar un agente sin que exista la gobernanza base (`00-B-02`), o si el nivel de autonomía solicitado para un agente entra en conflicto con las reglas comunes obligatorias, señalar el conflicto antes de generar la configuración específica
- Siguiente: `00-C-02-plan-mode-multiagente`

### 0-D.1 — Project Charter: Definición formal de proyecto nuevo
- Archivo: [references/00-D-01-project-charter.md](references/00-D-01-project-charter.md)
- Cuándo usarlo: al inicio de un proyecto nuevo, al formalizar un proyecto que comenzó sin documentación, o al actualizar el alcance después de un cambio estratégico significativo.
- Entradas: nombre y tipo de proyecto, patrocinador, cliente/usuario final, contexto o necesidad de negocio, stack tecnológico preliminar, restricciones conocidas, supuestos clave
- Autonomía permitida: A1 — Proponer (el documento requiere firma/aprobación humana explícita en el apartado 12 antes de considerarse vigente)
- Detente si: si falta información crítica para un apartado (patrocinador, alcance, presupuesto) que no pueda inferirse razonablemente de las entradas, marcarla con `[PENDIENTE: razón]` en vez de inventar cifras, fechas o compromisos
- Siguiente: `00-D-02-stack-arquitectura-inicial`, `00-B-01-scaffolding-repositorio`

### 0-D.2 — Stack y Arquitectura Inicial: Selección y documentación del fundamento técnico
- Archivo: [references/00-D-02-stack-arquitectura-inicial.md](references/00-D-02-stack-arquitectura-inicial.md)
- Cuándo usarlo: después de aprobar el Project Charter (`00-D-01`) y antes de generar los ADRs individuales (`04-04-adr-decisiones-arquitectura.md`), la estructura del repositorio (`00-B-01`) o el plan de implementación (`05-01-plan-implementacion.md`).
- Entradas: nombre del proyecto y descripción del dominio, tipo de sistema, restricciones conocidas (incluye compliance), stack preliminar si existe, escala esperada, plataforma de despliegue, composición del equipo; requiere que el Project Charter (`00-D-01`) ya esté ap…
- Autonomía permitida: A1 — Proponer (decisiones marcadas `[DECISIÓN PENDIENTE]` o `[ADR REQUERIDO]` no se consideran aplicadas hasta que exista un ADR formal y aprobación posterior)
- Detente si: si una decisión de seguridad, compliance o escalabilidad no puede justificarse con la información disponible, marcarla como `[DECISIÓN PENDIENTE: razón]` y `[ADR REQUERIDO]` en vez de asumir una elección definitiva sin evidencia
- Siguiente: `04-04-adr-decisiones-arquitectura` (skill `sdlc-diseno`), `00-B-01-scaffolding-repositorio`

### 0-D.3 — Plan de trabajo del proyecto: cronograma, EDT y asignación de recursos
- Archivo: [references/00-D-03-plan-trabajo-proyecto.md](references/00-D-03-plan-trabajo-proyecto.md)
- Cuándo usarlo: después de aprobar el Project Charter (`00-D-01`) y, si ya existe, el stack/arquitectura inicial (`00-D-02`) — antes de iniciar la ejecución del proyecto, para tener un cronograma y una asignación de recursos que el equipo o patrocinador pueda aprobar.
- Entradas: Project Charter aprobado (`00-D-01`), alcance y entregables principales, equipo disponible (roles, capacidad, calendario), fecha límite o ventana objetivo si existe, dependencias externas conocidas (otros equipos, proveedores, aprobaciones)
- Autonomía permitida: A1 — Proponer (cronograma y asignación de recursos quedan marcados como propuesta hasta aprobación del patrocinador o equipo)
- Detente si: si la fecha límite declarada no es alcanzable con el equipo y alcance dados, no ajustar las estimaciones para que "encajen" — reportarlo explícitamente como conflicto con las opciones de trade-off; si falta información de capacidad del equipo, detener y solicitarla antes de asignar recursos
- Siguiente: `05-02-riesgos-implementacion` (skill `sdlc-planificacion`), `05-01-plan-implementacion` (skill `sdlc-planificacion`)

### 0-D.4 — Registro de riesgos del proyecto (RAID): riesgos, supuestos, incidentes y dependencias
- Archivo: [references/00-D-04-registro-riesgos-proyecto.md](references/00-D-04-registro-riesgos-proyecto.md)
- Cuándo usarlo: junto con el Project Charter (`00-D-01`) y el plan de trabajo (`00-D-03`), al inicio del proyecto, y revisado periódicamente (cada hito o cada sprint) durante toda la ejecución — un registro de riesgos que solo se llena una vez al inicio pierde su valor.
- Entradas: Project Charter (`00-D-01`), stack/arquitectura inicial (`00-D-02`) si existe, plan de trabajo (`00-D-03`) si existe, restricciones de negocio conocidas, historial de riesgos materializados en proyectos similares si existe
- Autonomía permitida: A0 — Analizar (riesgos, supuestos, incidentes y dependencias ya declarados o evidentes en el contexto); A1 — Proponer (mitigaciones, riesgos inferidos no declarados explícitamente por el negocio, siempre marcados como propuesta)
- Detente si: si un riesgo queda clasificado como alto (probabilidad alta o impacto alto) sin una mitigación viable, no lo minimices ni lo dejes implícito — decláralo explícitamente como bloqueante para aprobar el Charter o el plan de trabajo
- Siguiente: `05-02-riesgos-implementacion` (skill `sdlc-planificacion`)

### 0-D.5 — Estudio de viabilidad y business case: ¿deberíamos hacer este proyecto?
- Archivo: [references/00-D-05-viabilidad-business-case.md](references/00-D-05-viabilidad-business-case.md)
- Cuándo usarlo: al recibir una idea de proyecto o iniciativa de negocio, **antes** de `00-D-01-project-charter` — este prompt determina si el proyecto debería formalizarse; el Charter asume que ya se decidió que sí.
- Entradas: idea o iniciativa en bruto, contexto de negocio, restricciones conocidas (presupuesto máximo, plazo, recursos disponibles), alternativas ya consideradas si existen
- Autonomía permitida: A1 — Proponer
- Detente si: si no puede estimarse ni el costo ni el beneficio con un mínimo de confianza, no forzar una recomendación go/no-go — declarar "viabilidad no determinable con la información disponible" en vez de inventar una cifra
- Siguiente: `00-D-01-project-charter`

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
