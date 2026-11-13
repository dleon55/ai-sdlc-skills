---
name: sdlc-seguridad
description: "Prompts AI-SDLC de seguridad. Úsala para trabajo de seguridad autorizado: SAST, análisis de dependencias (SCA), revisión de Secure SDLC, modelado de amenazas, DAST, pruebas de penetración con autorización, gestión de vulnerabilidades y CVE, gestión de secretos o evaluación de impacto de privacidad (DPIA)."
license: CC-BY-4.0
---

# Fase AI-SDLC 13 — Seguridad

Esta skill agrupa los prompts de la fase **Seguridad** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 13.1 — SAST: Análisis estático de seguridad de código
- Archivo: [references/13-01-sast-analisis-seguridad-codigo.md](references/13-01-sast-analisis-seguridad-codigo.md)
- Cuándo usarlo: antes de abrir un PR, después de implementar un cambio con implicaciones de seguridad, o como revisión periódica del código base. Complementa (no reemplaza) a herramientas automáticas de SAST.
- Entradas: código fuente y rama a analizar, lenguaje/framework, modelo de autenticación en uso, tipo de datos sensibles manejados; resultado de `13-04` (Threat Modeling) si existe
- Autonomía permitida: A0 — Analizar
- Detente si: si no se puede determinar el lenguaje, framework o los puntos de entrada de datos, declararlo explícitamente en vez de inventar hallazgos; no reclasificar severidad sin evidencia de código citada
- Siguiente: `13-07-gestion-vulnerabilidades-cves`, `08-03-remediacion-maestro` (skill `sdlc-revision`)

### 13.2 — SCA: Análisis de composición de software y dependencias
- Archivo: [references/13-02-sca-analisis-dependencias.md](references/13-02-sca-analisis-dependencias.md)
- Cuándo usarlo: en cada PR que modifique dependencias, como revisión periódica (al menos mensual), antes de un release a producción, y como respuesta a alertas de seguridad publicadas (GitHub Dependabot, OSS-Index, etc.).
- Entradas: archivos de gestión de dependencias y lock files del proyecto (package.json, requirements.txt, go.mod, etc.), tipo de producto (comercial/open source/interno) para el análisis de licencias; hallazgos previos de `13-07` si existen
- Autonomía permitida: A0 — Analizar
- Detente si: si no hay acceso a lock files, declarar el análisis como incompleto e indicar qué falta en vez de simular CVEs inexistentes; escalar a legal/compliance ante licencias problemáticas o sin licencia detectada
- Siguiente: `13-07-gestion-vulnerabilidades-cves`

### 13.3 — Revisión de desarrollo de software seguro (Secure SDLC)
- Archivo: [references/13-03-secure-sdlc-revision.md](references/13-03-secure-sdlc-revision.md)
- Cuándo usarlo: al cierre de cada sprint, antes de un release a producción, como revisión de madurez de seguridad del proyecto, o cuando se incorpora un nuevo equipo o agente al proyecto.
- Entradas: fase actual del ciclo, resultados disponibles de `13-01` (SAST), `13-02` (SCA) y `13-04` (Threat Modeling), arquitectura y workflows CI/CD del proyecto
- Autonomía permitida: A0 — Analizar el estado de cada control; A1 — Proponer el plan de mejora y el roadmap de madurez priorizado
- Detente si: marcar un control como "⚠️ parcial" o "❌ no cumple" en vez de "✅ cumple" si no hay evidencia verificable citada; detener y escalar si se detecta un secreto en código o un control crítico ausente en producción
- Siguiente: `08-03-remediacion-maestro` (skill `sdlc-revision`), `05-01-plan-implementacion` (skill `sdlc-planificacion`), `13-05-dast-analisis-dinamico-seguridad`

### 13.4 — Modelado de amenazas (Threat Modeling)
- Archivo: [references/13-04-threat-modeling.md](references/13-04-threat-modeling.md)
- Cuándo usarlo: en la fase de diseño de nuevas funcionalidades con impacto en seguridad, al diseñar integraciones con sistemas externos, al cambiar el modelo de autenticación o autorización, o al incorporar manejo de datos sensibles.
- Entradas: descripción del sistema/componente a modelar, diseño de solución (`04-01`) o casos de uso (`04-03`) si existen, diagramas de arquitectura o flujo (`04-02`), modelo de autenticación y datos sensibles involucrados
- Autonomía permitida: A0 — Analizar el diseño y generar el modelo de amenazas STRIDE
- Detente si: no inventar componentes, flujos o integraciones que no estén descritos en el diseño o código real; si no hay diseño disponible, solicitarlo antes de modelar amenazas especulativas
- Siguiente: `13-01-sast-analisis-seguridad-codigo`

### 13.5 — DAST: Análisis dinámico de seguridad de aplicación
- Archivo: [references/13-05-dast-analisis-dinamico-seguridad.md](references/13-05-dast-analisis-dinamico-seguridad.md)
- Cuándo usarlo: cuando la aplicación pueda levantarse en un entorno aislado (local, staging, Docker), antes de promover a producción, o como parte del pipeline CI/CD en la fase de validación de seguridad. Complementa al análisis estático (`13-01` SAST) y al modelo de amenazas (`13-04`).
- Entradas: entorno de pruebas aislado (URL base), stack, tipo de aplicación, mecanismo de autenticación; resultados de `13-04` y `13-01` si existen
- Autonomía permitida: A2 — Ejecutar controlado, limitado al entorno aislado declarado como entrada
- Detente si: nunca ejecutar contra producción sin autorización explícita y documentada; detener si el entorno de pruebas no está confirmado como aislado
- Siguiente: `13-06-ethical-hacking-pentesting`, `08-03-remediacion-maestro` (skill `sdlc-revision`)

### 13.6 — Ethical Hacking y Pruebas de Penetración
- Archivo: [references/13-06-ethical-hacking-pentesting.md](references/13-06-ethical-hacking-pentesting.md)
- Cuándo usarlo: antes de lanzamientos mayores, después de cambios significativos en la arquitectura, para cumplimiento de estándares (PCI-DSS, ISO 27001, SOC 2), o como ejercicio periódico de validación de seguridad. Requiere autorización explícita y entorno aislado.
- Entradas: alcance autorizado explícito (dominios/IPs/sistemas incluidos y excluidos), entorno de prueba, tipo de caja, resultados previos de `13-04`/`13-01`/`13-05` si existen
- Autonomía permitida: A2 — Ejecutar controlado, solo dentro del alcance y ventana de tiempo autorizados por escrito
- Detente si: requiere autorización explícita del propietario del sistema antes de cualquier técnica de explotación; nunca ejecutar acciones destructivas, DoS/DDoS o ingeniería social sobre personas reales
- Siguiente: `08-03-remediacion-maestro` (skill `sdlc-revision`)

### 13.7 — Análisis de vulnerabilidades y gestión de CVEs
- Archivo: [references/13-07-gestion-vulnerabilidades-cves.md](references/13-07-gestion-vulnerabilidades-cves.md)
- Cuándo usarlo: después de ejecutar cualquier herramienta de análisis de seguridad (`13-01` SAST, `13-02` SCA, `13-05` DAST, `13-06` pentesting), al recibir alertas de nuevos CVEs que afectan las dependencias del proyecto, o como revisión periódica del estado de seguridad.
- Entradas: reportes de las herramientas de seguridad ejecutadas (`13-01`, `13-02`, `13-05`, `13-06` o escáneres automáticos), criticidad del sistema afectado, SLAs de remediación definidos por el proyecto (o usar los estándar)
- Autonomía permitida: A1 — Proponer el backlog de seguridad priorizado, sin crear issues ni aplicar cambios directamente
- Detente si: no clasificar un hallazgo como falso positivo o aceptado con riesgo sin documentar el razonamiento y, en el caso de "aceptado con riesgo", sin aprobación y fecha de revisión explícitas; si existe exploit público activo, escalar el SLA a inmediato sin excepción
- Siguiente: `08-03-remediacion-maestro` (skill `sdlc-revision`)

### 13.8 — Gestión de Secretos y Credenciales
- Archivo: [references/13-08-gestion-secretos-credenciales.md](references/13-08-gestion-secretos-credenciales.md)
- Cuándo usarlo: como revisión preventiva antes de un PR, tras recibir alertas de escaneo de secretos (GitHub Secret Scanning, Gitleaks, truffleHog), al incorporarse al proyecto para auditar el estado histórico, o como parte de la revisión Secure SDLC (`13-03`).
- Entradas: stack tecnológico, gestor de secretos actual, CI/CD usado, proveedores de servicio con credenciales, profundidad de análisis de historial Git
- Autonomía permitida: A0 — Analizar para el inventario y clasificación; A1 — Proponer para el plan de remediación; nunca A2/A3 automático para revocar/rotar secretos o reescribir historia sin aprobación
- Detente si: nunca incluir el valor real de un secreto detectado en la salida, solo su ubicación y tipo; detener antes de ejecutar `git filter-repo` sin coordinación explícita del equipo (requiere push forzado)
- Siguiente: `13-03-secure-sdlc-revision`

### 13.9 — Evaluación de impacto de privacidad de datos (DPIA)
- Archivo: [references/13-09-dpia-privacidad-datos.md](references/13-09-dpia-privacidad-datos.md)
- Cuándo usarlo: al diseñar una funcionalidad que procesa datos personales o sensibles nuevos, o antes de un cambio significativo en cómo se procesan datos ya existentes.
- Entradas: descripción de los datos personales/sensibles procesados, propósito del procesamiento, base legal propuesta, terceros involucrados (procesadores/subencargados), ubicación geográfica de los usuarios y del almacenamiento
- Autonomía permitida: A0 — Analizar; A1 — Proponer (base legal sugerida, controles de mitigación)
- Detente si: si no puede determinarse una base legal válida para el procesamiento, no asumas una — repórtalo como bloqueante que requiere decisión legal antes de continuar
- Siguiente: `13-04-threat-modeling`, `13-08-gestion-secretos-credenciales`

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
