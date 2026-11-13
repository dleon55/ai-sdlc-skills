---
name: sdlc-pruebas
description: "Prompts AI-SDLC de pruebas. Úsala cuando pidan diseñar o implementar pruebas: unitarias, de integración, E2E, de humo, de rendimiento y carga, accesibilidad, diagnóstico de pruebas inestables (flaky), datos de prueba, detección del stack de pruebas o plan maestro de pruebas."
license: CC-BY-4.0
---

# Fase AI-SDLC 07 — Pruebas

Esta skill agrupa los prompts de la fase **Pruebas** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 7.0 — Detección de stack de pruebas
- Archivo: [references/07-00-deteccion-stack-pruebas.md](references/07-00-deteccion-stack-pruebas.md)
- Cuándo usarlo: una sola vez por proyecto, o cuando el stack de pruebas cambie. El perfil generado se reutiliza en todas las ejecuciones de los prompts de implementación de pruebas.
- Entradas: acceso de lectura al repositorio: archivos de configuración raíz (package.json, pyproject.toml, pom.xml, etc.), workflows de CI/CD, directorio de pruebas existente
- Autonomía permitida: A0 — Analizar (lectura e inventario); no aplica cambios ni requiere aprobación
- Detente si: marcar explícitamente "sin detectar" en vez de asumir o inventar un framework, comando o convención que no esté respaldado por un archivo real del repositorio
- Siguiente: `07-01-pruebas-unitarias`, `07-07-implementacion-pruebas-unitarias`, `07-15-plan-maestro-pruebas`

### 7.1 — Diseño de pruebas unitarias
- Archivo: [references/07-01-pruebas-unitarias.md](references/07-01-pruebas-unitarias.md)
- Cuándo usarlo: después de implementar cambios, en paralelo a la implementación, o como referencia antes de escribir código.
- Entradas: código implementado o cambios propuestos, criterios de aceptación, perfil de stack de pruebas (`07-00`) si está disponible
- Autonomía permitida: A1 — Proponer (matriz de pruebas como artefacto, sin implementar el código de test)
- Detente si: detener si no hay código o criterios de aceptación de referencia; señalar explícitamente si la cobertura recomendada no puede alcanzarse con la información disponible en vez de inventar escenarios
- Siguiente: `07-07-implementacion-pruebas-unitarias`

### 7.2 — Diseño de pruebas de integración
- Archivo: [references/07-02-pruebas-integracion.md](references/07-02-pruebas-integracion.md)
- Cuándo usarlo: después de las pruebas unitarias (`07-01`), para validar que los módulos funcionan correctamente en conjunto.
- Entradas: contratos de API, diseño de integración, datos de prueba disponibles, matriz de pruebas unitarias (`07-01`) si existe
- Autonomía permitida: A1 — Proponer (plan de pruebas de integración sin implementar)
- Detente si: detener si faltan contratos de API o diseño de integración de referencia; nunca usar datos reales de producción como datos de prueba, solo datos sintéticos o anonimizados
- Siguiente: `07-08-implementacion-pruebas-integracion`

### 7.3 — Diseño de pruebas E2E
- Archivo: [references/07-03-pruebas-e2e.md](references/07-03-pruebas-e2e.md)
- Cuándo usarlo: después de las pruebas de integración (`07-02`), para validar el flujo completo desde la perspectiva del usuario.
- Entradas: caso de uso o requerimiento a cubrir, criterios de aceptación, referencia al plan de integración previo (`07-02`)
- Autonomía permitida: A1 — Proponer (entrega un plan/artefacto sin aplicar; la ejecución ocurre en `07-09`)
- Detente si: detener y pedir aclaración si el caso de uso o los criterios de aceptación no están definidos con suficiente detalle para derivar pasos, resultado esperado y evidencia
- Siguiente: `07-09-implementacion-pruebas-e2e`

### 7.4 — Pruebas de humo
- Archivo: [references/07-04-pruebas-humo.md](references/07-04-pruebas-humo.md)
- Cuándo usarlo: inmediatamente después de un despliegue o merge, para una validación rápida de salud del sistema antes de pruebas completas.
- Entradas: flujos críticos documentados, referencia a la rama o versión desplegada, ambiente objetivo (QA/STAGING/PROD)
- Autonomía permitida: A1 — Proponer (entrega un checklist priorizado como artefacto, sin ejecutarlo contra el sistema)
- Detente si: detener si no hay flujos críticos identificados o si el ambiente objetivo no está definido, ya que el checklist perdería su utilidad como validación rápida
- Siguiente: `07-10-implementacion-pruebas-humo`

### 7.5 — Automatización en navegador con Google Antigravity
- Archivo: [references/07-05-automatizacion-antigravity.md](references/07-05-automatizacion-antigravity.md)
- Cuándo usarlo: para automatizar pruebas E2E o de regresión de flujos críticos impactados por el cambio. Usa este prompt en lugar de `07-03`+`07-09` cuando la automatización se ejecutará mediante el agente de navegador de Google Antigravity (verificación autónoma con capturas/video) en vez de un framework de scripting E2E tradicional.
- Entradas: casos de uso o flujos críticos a automatizar, plan E2E previo si existe, diseño de UI, URL base del ambiente QA/STAGING
- Autonomía permitida: A1 — Proponer (entrega la estrategia como artefacto; la ejecución autónoma por Google Antigravity es un paso externo posterior que requiere ambiente y credenciales de prueba ya autorizados)
- Detente si: detener si el ambiente de destino no es QA/STAGING (nunca automatizar directamente contra producción); detener si faltan selectors o datos de prueba estables, ya que produciría una automatización frágil

### 7.6 — Pruebas de performance y carga
- Archivo: [references/07-06-pruebas-performance-carga.md](references/07-06-pruebas-performance-carga.md)
- Cuándo usarlo: antes de desplegar a producción cambios que afecten APIs, consultas de base de datos, procesos batch, generación de archivos o cualquier componente con requerimientos de rendimiento. También como revisión periódica de salud del sistema.
- Entradas: componentes a probar, ambiente de prueba (QA/Staging — nunca producción), usuarios concurrentes esperados en producción, SLA o tiempo de respuesta aceptable, herramienta disponible (k6/Locust/JMeter/Artillery/hey/wrk)
- Autonomía permitida: A1 — Proponer (estrategia, escenarios y script base) — este prompt nunca ejecuta pruebas de carga bajo ninguna autonomía; la ejecución (incluso en QA/Staging con aprobación) es responsabilidad exclusiva de `07-11-implementacion-pruebas-performance`
- Detente si: detener y escalar si el ambiente propuesto es producción; no ejecutar la prueba si no hay SLA o umbrales de fallo definidos; nunca usar datos reales de usuarios o de producción en los payloads de prueba
- Siguiente: `07-11-implementacion-pruebas-performance`

### 7.7 — Implementación de pruebas unitarias
- Archivo: [references/07-07-implementacion-pruebas-unitarias.md](references/07-07-implementacion-pruebas-unitarias.md)
- Cuándo usarlo: después de completar el diseño de pruebas unitarias (`07-01`), cuando el agente tiene acceso al código fuente y al framework de pruebas del proyecto.
- Entradas: Perfil de stack de pruebas (`07-00`) y matriz de diseño de pruebas unitarias (`07-01`) adjuntos o referenciados; acceso al código fuente de las unidades bajo prueba
- Autonomía permitida: A2 — Ejecutar controlado (escribe y ejecuta archivos de prueba en el workspace, sin publicar cambios)
- Detente si: no modificar código fuente bajo ningún concepto; detener tras un máximo de 3 ciclos de auto-corrección si persisten fallos de compilación o asserts, y reportar el diagnóstico exacto en vez de seguir intentando
- Siguiente: `07-08-implementacion-pruebas-integracion`

### 7.8 — Implementación de pruebas de integración
- Archivo: [references/07-08-implementacion-pruebas-integracion.md](references/07-08-implementacion-pruebas-integracion.md)
- Cuándo usarlo: después de completar el diseño de pruebas de integración (`07-02`), cuando el entorno de pruebas (base de datos, servicios dependientes) está disponible o puede ser simulado con contenedores o stubs.
- Entradas: Perfil de stack de pruebas (`07-00`) y plan de pruebas de integración (`07-02`) adjuntos o referenciados; entorno de pruebas disponible o simulable (contenedores, stubs)
- Autonomía permitida: A2 — Ejecutar controlado (escribe, ejecuta y limpia estado en workspace o entorno de pruebas aislado)
- Detente si: detener si una dependencia externa requerida no puede simularse con stub o contenedor y la prueba dependería de un servicio real de producción; detener si el teardown no puede garantizar el aislamiento del estado entre ejecuciones
- Siguiente: `07-09-implementacion-pruebas-e2e`

### 7.9 — Implementación de pruebas E2E
- Archivo: [references/07-09-implementacion-pruebas-e2e.md](references/07-09-implementacion-pruebas-e2e.md)
- Cuándo usarlo: después de completar el diseño de pruebas E2E (`07-03`), cuando la aplicación está desplegada en un entorno de pruebas accesible (QA o staging).
- Entradas: Perfil de stack de pruebas (`07-00`) y plan de pruebas E2E (`07-03`) adjuntos o referenciados; aplicación desplegada y accesible en un entorno de pruebas (QA/staging) con credenciales de prueba
- Autonomía permitida: A2 — Ejecutar controlado (ejecuta scripts contra un entorno de pruebas aislado, nunca contra producción)
- Detente si: detener si la URL objetivo apunta a producción; detener si el flujo requeriría datos reales de usuarios; detener y documentar si el cleanup del estado generado (registros creados) no puede garantizarse al finalizar el test
- Siguiente: `07-04-pruebas-humo`, `07-10-implementacion-pruebas-humo`

### 7.10 — Implementación de pruebas de humo
- Archivo: [references/07-10-implementacion-pruebas-humo.md](references/07-10-implementacion-pruebas-humo.md)
- Cuándo usarlo: después de completar el diseño de pruebas de humo (`07-04`), como paso inmediato post-despliegue para decidir si el ambiente está listo para pruebas completas o requiere rollback.
- Entradas: checklist de pruebas de humo generado por `07-04`, Perfil de stack de pruebas de `07-00`, endpoints de salud o flujos críticos documentados
- Autonomía permitida: A2 — Ejecutar controlado
- Detente si: si el checklist de `07-04` no existe o está incompleto, o si algún check requeriría escribir o modificar datos de negocio para verificarse, detener y escalar en vez de improvisar el check
- Siguiente: `09-04-promotion-checklist` (skill `sdlc-integracion`)

### 7.11 — Implementación de pruebas de performance y carga
- Archivo: [references/07-11-implementacion-pruebas-performance.md](references/07-11-implementacion-pruebas-performance.md)
- Cuándo usarlo: después de completar el diseño de pruebas de performance (`07-06`), cuando ya existe el ambiente de prueba levantado (QA / staging) y se necesita el script ejecutable para la herramienta seleccionada.
- Entradas: diseño de pruebas de performance de `07-06` (escenarios, umbrales, herramienta seleccionada), Perfil de stack de pruebas de `07-00`, URL del ambiente de prueba y esquema de autenticación
- Autonomía permitida: A2 — Ejecutar controlado para load/benchmark en staging; A3 explícito y ventana de mantenimiento aprobada para cualquier ejecución de stress/spike/soak contra producción
- Detente si: si no hay un ambiente de staging disponible, si la URL base apunta a producción sin ventana de mantenimiento confirmada, o si las credenciales provistas no son de datos sintéticos/prueba, detener y escalar
- Siguiente: `11-05-performance-produccion-diagnostico` (skill `sdlc-operaciones`)

### 7.12 — Auditoría de Accesibilidad (a11y) y UX Compliance
- Archivo: [references/07-12-accessibility-a11y-audit.md](references/07-12-accessibility-a11y-audit.md)
- Cuándo usarlo: Antes de fusionar un Pull Request que introduce o modifica componentes visuales del Frontend, o al auditar un sistema existente para cumplir normativas de accesibilidad.
- Entradas: código fuente del componente o vista (`codigo_frontend`) y el framework UI usado (`framework_ui`)
- Autonomía permitida: A1 — Proponer (entrega informe y código corregido como propuesta; no aplica el cambio directamente al repositorio)
- Detente si: si el fragmento de código no incluye suficiente contexto para evaluar un criterio (p. ej.
- Siguiente: `08-01-revision-completa-pr` (skill `sdlc-revision`)

### 7.13 — Diagnóstico y estabilización de tests inestables (flaky)
- Archivo: [references/07-13-diagnostico-tests-flaky.md](references/07-13-diagnostico-tests-flaky.md)
- Cuándo usarlo: cuando un test ya existente falla intermitentemente en CI o localmente sin cambios de código aparentes, antes de decidir si se ignora, se reintenta automáticamente o se corrige de raíz.
- Entradas: nombre/ruta del test, historial de ejecuciones recientes en CI (pasa/falla, timestamps), logs o stack traces de al menos 2-3 fallas, código del test y del código bajo prueba relacionado, indicación de si falla también en local o solo en CI
- Autonomía permitida: A0 — Analizar (diagnóstico de causa); A1 — Proponer (fix, cuarentena o eliminación); A2 — Ejecutar controlado solo para correr el test repetidamente en un ambiente aislado con el propósito de reproducir el patrón, nunca para aplicar el fix sin revisión humana
- Detente si: si no se puede reproducir la falla tras el número de corridas definido en el protocolo, declarar "no reproducido" en vez de adivinar la causa; nunca recomendar cuarentena permanente sin un ticket de seguimiento con fecha de revisión
- Siguiente: `11-03-deuda-tecnica` (skill `sdlc-operaciones`)

### 7.14 — Estrategia de gestión de datos de prueba en QA
- Archivo: [references/07-14-gestion-datos-prueba.md](references/07-14-gestion-datos-prueba.md)
- Cuándo usarlo: al configurar un ambiente de QA/staging compartido nuevo, o cuando aparecen fallas de pruebas por datos inconsistentes/contaminados entre corridas o por colisión entre ejecuciones paralelas.
- Entradas: ambiente(s) de prueba a cubrir, origen del dataset (sintético / snapshot de producción enmascarado / mixto), volumen de datos necesario para representatividad, cantidad de pipelines/agentes ejecutando en paralelo, política de compliance aplicable a los datos…
- Autonomía permitida: A1 — Proponer (estrategia y scripts); A2 — Ejecutar controlado solo en el ambiente de prueba aislado indicado, nunca contra producción ni contra un ambiente compartido sin aprobación explícita
- Detente si: detener si se pide partir de un snapshot de producción sin una política de enmascarado de PII/datos sensibles ya definida — no diseñar el enmascarado por cuenta propia sin esa política; detener si no se puede confirmar el volumen de datos necesario para que las pruebas sean representativas
- Siguiente: `13-08-gestion-secretos-credenciales` (skill `sdlc-seguridad`)

### 7.15 — Plan maestro de pruebas: estrategia de QA del proyecto
- Archivo: [references/07-15-plan-maestro-pruebas.md](references/07-15-plan-maestro-pruebas.md)
- Cuándo usarlo: al inicio de un proyecto (después de `07-00`, detección del stack de pruebas) o al planificar un release/hito mayor, antes de diseñar pruebas individuales por tipo (`07-01` a `07-06`).
- Entradas: perfil de stack de pruebas (`07-00`) si existe, alcance del proyecto o release, requerimientos no funcionales relevantes (`02-06`) si existen, restricciones de tiempo/recursos de QA, ambientes disponibles
- Autonomía permitida: A1 — Proponer
- Detente si: si no puede definirse un criterio de salida objetivo y verificable para al menos los niveles críticos (unitaria, integración, E2E de los flujos core), no declares la estrategia como completa — repórtalo como vacío pendiente en vez de rellenarlo con un criterio subjetivo
- Siguiente: `07-01-pruebas-unitarias`

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
