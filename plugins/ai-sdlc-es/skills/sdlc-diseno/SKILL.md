---
name: sdlc-diseno
description: "Prompts AI-SDLC de diseño de la solución. Úsala cuando haya que diseñar antes de implementar: diseño de solución, diagramas Mermaid, casos de uso, ADR (decisiones de arquitectura), contrato de API, versionado y deprecación de API o modelo de datos."
license: CC-BY-4.0
---

# Fase AI-SDLC 04 — Diseño de la solución

Esta skill agrupa los prompts de la fase **Diseño de la solución** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 4.1 — Diseño funcional y técnico de solución
- Archivo: [references/04-01-diseno-solucion.md](references/04-01-diseno-solucion.md)
- Cuándo usarlo: una vez completado el análisis funcional, técnico y de impacto, antes de planificar o ejecutar cualquier cambio.
- Entradas: análisis funcional, técnico y de impacto cruzado ya completados (`02-01`, `02-02`, `02-03`), arquitectura y contratos existentes
- Autonomía permitida: A1 — Proponer
- Detente si: si no existe una estrategia de rollback viable para un componente crítico, declararlo como riesgo abierto en el diseño en vez de omitirlo
- Siguiente: `05-01-plan-implementacion` (skill `sdlc-planificacion`), `04-02-diagramas-mermaid`, `04-06-diseno-contrato-api`, `04-07-diseno-modelo-datos`

### 4.2 — Generar diagramas Mermaid
- Archivo: [references/04-02-diagramas-mermaid.md](references/04-02-diagramas-mermaid.md)
- Cuándo usarlo: durante o después del diseño de la solución (`04-01`), para documentar y comunicar visualmente los cambios.
- Entradas: diseño aprobado (`04-01`), arquitectura real del sistema, código fuente o componentes involucrados en el cambio
- Autonomía permitida: A0 — Analizar el diseño y código existente; A1 — Proponer los diagramas como artefacto de documentación
- Detente si: detener si no existe diseño aprobado (`04-01`) del cual derivar los diagramas; nunca inventar componentes, actores o flujos que no existan en el código o diseño real
- Siguiente: `04-03-casos-de-uso`

### 4.3 — Diseño de casos de uso
- Archivo: [references/04-03-casos-de-uso.md](references/04-03-casos-de-uso.md)
- Cuándo usarlo: durante la fase de diseño, para formalizar el comportamiento esperado del sistema antes de implementar.
- Entradas: análisis funcional previo (`02-01`), documentación existente de casos de uso, módulo o funcionalidad objetivo
- Autonomía permitida: A1 — Proponer
- Detente si: si faltan reglas de negocio, postcondiciones o criterios de aceptación verificables para un flujo, marcarlo como pendiente de validación funcional en vez de inventarlos
- Siguiente: `04-04-adr-decisiones-arquitectura`, `05-01-plan-implementacion` (skill `sdlc-planificacion`)

### 4.4 — Architecture Decision Records (ADR)
- Archivo: [references/04-04-adr-decisiones-arquitectura.md](references/04-04-adr-decisiones-arquitectura.md)
- Cuándo usarlo: al tomar una decisión arquitectónica significativa (elección de tecnología, patrón de diseño, estrategia de integración, estructura de datos), al documentar decisiones pasadas que no quedaron registradas, o como revisión al inicio de un proyecto.
- Entradas: contexto del problema, opciones evaluadas, decisión ya tomada (este prompt documenta, no decide)
- Autonomía permitida: A1 — Proponer
- Detente si: antes de asignar el número, verificar `docs/decisions/README.md` o el índice existente para evitar colisión con un ADR-NNN ya usado
- Siguiente: `05-01-plan-implementacion` (skill `sdlc-planificacion`)

### 4.5 — Versionado y deprecación de API
- Archivo: [references/04-05-versionado-deprecacion-api.md](references/04-05-versionado-deprecacion-api.md)
- Cuándo usarlo: cuando un cambio en una API rompe (o puede romper) el contrato existente con sus consumidores — renombrar/eliminar campos, cambiar tipos, modificar autenticación, cambiar códigos de estado o semántica de un endpoint — y hace falta decidir cómo introducirlo sin dejar a los clientes sin aviso.
- Entradas: endpoint(s) u operación afectada, naturaleza del cambio propuesto, consumidores conocidos de la API (internos/externos, si se conocen), política de versionado existente del proyecto (si existe), SLA o acuerdos de soporte vigentes con consumidores
- Autonomía permitida: A1 — Proponer
- Detente si: detener y escalar si no se puede determinar si el cambio es breaking o no; detener si se desconoce por completo la base de consumidores y el prompt no puede señalar explícitamente ese vacío; nunca proponer eliminar una versión sin período de aviso definido
- Siguiente: `09-06-coordinacion-breaking-changes` (skill `sdlc-integracion`)

### 4.6 — Diseño de contrato de API: endpoints, esquemas y semántica de interfaz
- Archivo: [references/04-06-diseno-contrato-api.md](references/04-06-diseno-contrato-api.md)
- Cuándo usarlo: después del diseño de solución (`04-01`) cuando este expone una API nueva, o como paso independiente cuando el requerimiento es explícitamente diseñar una interfaz.
- Entradas: diseño de solución (`04-01`) si existe, casos de uso relacionados (`04-03`) si existen, consumidores previstos (internos/externos), estilo de API (REST/GraphQL/gRPC/otro), convenciones ya existentes en el proyecto si las hay
- Autonomía permitida: A1 — Proponer
- Detente si: si el estilo de API (REST/GraphQL/gRPC) no está definido y no puede inferirse de convenciones ya existentes en el proyecto, preguntar antes de asumir uno; ninguna operación puede quedar sin su matriz de errores definida
- Siguiente: `04-05-versionado-deprecacion-api`, `05-01-plan-implementacion` (skill `sdlc-planificacion`), `07-02-pruebas-integracion` (skill `sdlc-pruebas`)

### 4.7 — Diseño detallado de modelo de datos: entidades, relaciones y esquema
- Archivo: [references/04-07-diseno-modelo-datos.md](references/04-07-diseno-modelo-datos.md)
- Cuándo usarlo: durante la fase de diseño (después de `04-01`, en paralelo o después de `04-03`), cuando el cambio o proyecto requiere un modelo de datos nuevo o una extensión significativa del existente — antes de escribir la migración real.
- Entradas: entidades y relaciones del dominio (o el diseño de solución `04-01` / casos de uso `04-03` de los que inferirlas), motor de base de datos (relacional/documental/otro), volumen y patrón de acceso esperado (lecturas vs.
- Autonomía permitida: A1 — Proponer
- Detente si: si el motor de base de datos o el patrón de acceso esperado no se conoce, detener y solicitarlo antes de proponer un esquema — la normalización y la estrategia de índices dependen directamente de esa información
- Siguiente: `08-05-revision-migracion-esquema-bd` (skill `sdlc-revision`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
