---
name: sdlc-operaciones
description: "Prompts AI-SDLC de operaciones y sre. Úsala en operación de sistemas en producción: troubleshooting, hardening, deuda técnica, respuesta a incidentes, rendimiento en producción, parches, postmortem y runbooks, rollback, costos de nube (FinOps), capacidad, decomiso de legado, ruido de alertas, guardias, migración o cutover y recuperación ante desastres."
license: CC-BY-4.0
---

# Fase AI-SDLC 11 — Operaciones y SRE

Esta skill agrupa los prompts de la fase **Operaciones y SRE** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 11.1 — Troubleshooting de ambiente
- Archivo: [references/11-01-troubleshooting.md](references/11-01-troubleshooting.md)
- Cuándo usarlo: cuando un servicio falla, un despliegue no funciona como esperado, o hay un problema de configuración en cualquier ambiente. Si el ambiente es PROD y hay impacto significativo en usuarios, usa `11-04-incident-response` en su lugar.
- Entradas: síntoma, ambiente (DEV/QA/STAGING/PROD), servicios involucrados, evidencias disponibles (logs, errores, capturas)
- Autonomía permitida: A0 — Analizar: diagnóstico e hipótesis; la ruta de resolución queda propuesta y pendiente de aprobación antes de pasar a A2
- Detente si: si el ambiente es PROD y hay impacto significativo en usuarios, debe detenerse y derivar a `11-04-incident-response` en vez de continuar el troubleshooting estándar
- Siguiente: `11-04-incident-response`, `03-02-causa-raiz` (skill `sdlc-incidentes`)

### 11.2 — Hardening y seguridad operativa
- Archivo: [references/11-02-hardening-seguridad.md](references/11-02-hardening-seguridad.md)
- Cuándo usarlo: periódicamente como revisión de seguridad, antes de un despliegue a producción, o cuando se detectan hallazgos de seguridad en code review.
- Entradas: docker-compose, configuración nginx, `.env` (estructura, no valores), workflows, permisos de GitHub, acceso de lectura al historial de commits recientes (git log)
- Autonomía permitida: A0 — Analizar (solo entrega hallazgos y plan de mitigación, no aplica cambios)
- Detente si: nunca incluir valores reales de secretos en la salida, aunque se detecten expuestos; referenciar solo ubicación y tipo
- Siguiente: `13-08-gestion-secretos-credenciales` (skill `sdlc-seguridad`), `13-03-secure-sdlc-revision` (skill `sdlc-seguridad`)

### 11.3 — Deuda técnica y mejora continua
- Archivo: [references/11-03-deuda-tecnica.md](references/11-03-deuda-tecnica.md)
- Cuándo usarlo: al cierre de un sprint, en revisiones técnicas periódicas, o cuando se quiere planificar mejoras estructurales del proyecto.
- Entradas: rama principal, componentes o módulos a analizar, acceso a código fuente, tests, configuración CI/CD, arquitectura y documentación
- Autonomía permitida: A0 — Analizar: inventario y recomendaciones, sin aplicar cambios
- Detente si: si no puede acceder a un área declarada como "a analizar" (módulo inexistente o fuera del repo), debe señalar la omisión en vez de completar la matriz con supuestos
- Siguiente: `05-01-plan-implementacion` (skill `sdlc-planificacion`), `11-06-gestion-parches-actualizaciones`

### 11.4 — Runbook de incident response en producción
- Archivo: [references/11-04-incident-response.md](references/11-04-incident-response.md)
- Cuándo usarlo: cuando se detecta un incidente activo en producción, para documentar el proceso de respuesta a posteriori, o para diseñar el runbook estándar del proyecto antes de que ocurra el primer incidente.
- Entradas: síntoma/alerta, sistema afectado, ambiente, hora de detección, fuente de detección, stack
- Autonomía permitida: A0 — Analizar en fases 1-3 y 6-7; A3 — Publicar en fase 4 (rollback, mitigación o mutación contra producción activa son despliegue/mutación remota según `00-framework.md`, no ejecución en workspace aislado), solo si el runbook ya autorizó la acción específica y con la aprobación explícita o política preautorizada que exige A3
- Detente si: el propio prompt exige detener toda operación de agentes IA en el repositorio y no desplegar código mientras el incidente esté activo
- Siguiente: `03-02-causa-raiz` (skill `sdlc-incidentes`), `11-07-sre-postmortem-runbook`

### 11.5 — Performance en Producción: Diagnóstico y Optimización
- Archivo: [references/11-05-performance-produccion-diagnostico.md](references/11-05-performance-produccion-diagnostico.md)
- Cuándo usarlo: cuando se detecta degradación de rendimiento en producción (alertas de latencia, quejas de usuarios, burn rate del SLO acelerado), tras incorporar observabilidad (`10-04`) y visualizar métricas real-time, o como revisión periódica de salud de rendimiento.
- Entradas: métricas/trazas/logs del período de degradación (de `10-04` o exportación de Grafana/Datadog/CloudWatch), stack tecnológico, infraestructura, SLO impactado; opcionalmente umbrales de `07-06`/`07-11`
- Autonomía permitida: A0 — Analizar en caracterización, análisis de trazas/logs y diagnóstico por capa; A1 — Proponer en el plan de optimización; A2 — Ejecutar controlado solo para profiling en staging o para aplicar optimizaciones ya aprobadas
- Detente si: si el profiling necesario solo puede ejecutarse en producción y no hay staging con tráfico espejado disponible, debe detenerse y solicitar aprobación explícita antes de perfilar en vivo
- Siguiente: `07-06-pruebas-performance-carga` (skill `sdlc-pruebas`), `10-04-observabilidad-instrumentacion` (skill `sdlc-documentacion`)

### 11.6 — Gestión de Parches y Actualizaciones
- Archivo: [references/11-06-gestion-parches-actualizaciones.md](references/11-06-gestion-parches-actualizaciones.md)
- Cuándo usarlo: como revisión periódica de actualizaciones pendientes (mensual/trimestral), al recibir alertas de CVE que afectan dependencias del proyecto (`13-02` SCA), o antes de un release mayor para garantizar componentes actualizados.
- Entradas: stack tecnológico, ambientes disponibles, contexto de vulnerabilidades (resultado de `13-02` SCA si existe), herramientas de CI/CD, automatización existente, última fecha de parches, SLAs de seguridad comprometidos
- Autonomía permitida: A0 — Analizar en inventario y clasificación; A1 — Proponer en el plan de aplicación agrupado; A2 — Ejecutar controlado en dev/staging; A3 — Publicar únicamente para el despliegue a producción, y solo con aprobación explícita del responsable de rollback
- Detente si: si una actualización MAJOR con breaking changes no ha permanecido estable en staging al menos 24h, si el criterio de rollback (tasa de error/P95) no está definido antes de desplegar a producción, o si no existe aprobación explícita y documentada del responsable de rollback antes de ejecutar el desp…
- Siguiente: `13-02-sca-analisis-dependencias` (skill `sdlc-seguridad`), `11-07-sre-postmortem-runbook`

### 11.7 — Post-Mortem Blameless y Generación de Runbook (SRE)
- Archivo: [references/11-07-sre-postmortem-runbook.md](references/11-07-sre-postmortem-runbook.md)
- Cuándo usarlo: Inmediatamente después de haber resuelto un incidente crítico o caída en producción (Fase 03 finalizada), para documentar el aprendizaje institucional.
- Entradas: datos crudos del incidente (timeline, logs, chat), resolución aplicada; opcionalmente resultado de análisis de causa raíz `03-02`
- Autonomía permitida: A1 — Proponer: entrega el documento post-mortem y el runbook propuesto; adoptarlo como runbook oficial operable por on-call requiere revisión humana (A3)
- Detente si: si el análisis de 5 porqués converge en atribuir la falla a una persona en vez de a un sistema o proceso, debe reformular el hallazgo en términos blameless antes de continuar; si faltan datos suficientes del incidente, debe señalarlo en vez de inventar la cronología
- Siguiente: `10-04-observabilidad-instrumentacion` (skill `sdlc-documentacion`), `11-06-gestion-parches-actualizaciones`

### 11.8 — Auditoría de FinOps y Eficiencia de Costos Cloud
- Archivo: [references/11-08-finops-cloud-cost-audit.md](references/11-08-finops-cloud-cost-audit.md)
- Cuándo usarlo: Antes de aprovisionar nueva infraestructura, durante revisiones periódicas de costos (billing), o al evaluar arquitecturas para migraciones a la nube.
- Entradas: código de infraestructura (Terraform, CDK, Kubernetes manifests) o descripción de arquitectura, proveedor cloud
- Autonomía permitida: A1 — Proponer
- Detente si: no recomendar Spot Instances o cambios de tier de almacenamiento para cargas de trabajo sin tolerancia a interrupciones sin señalar explícitamente ese riesgo
- Siguiente: `09-03-workflows-github-actions` (skill `sdlc-integracion`)

### 11.9 — Runbook de ejecución de rollback
- Archivo: [references/11-09-runbook-rollback.md](references/11-09-runbook-rollback.md)
- Cuándo usarlo: cuando un cambio desplegado recientemente está causando problemas y se está considerando o ejecutando un rollback.
- Entradas: síntoma que motiva el rollback, componente(s) afectados y su tipo de cambio (código / migración de BD / config o feature flag / infraestructura), versión o estado objetivo al que revertir, indicación de si hubo escrituras de datos en la versión nueva, ambiente
- Autonomía permitida: A1 — Proponer para todo el diseño del criterio de decisión y del runbook de rollback; A2 — Ejecutar controlado solo para la ejecución en un ambiente aislado (staging/QA) con las precondiciones explícitas ya verificadas (versión previa confirmada desplegable, reversibilidad de la migración confirmada); A3 — Publicar para ejecutar el rollback contra producción, y en particular cualquier rollback que toque una migración de base de datos o datos de producción — es despliegue/mutación remota según `00-framework.md`, no ejecución en workspace aislado, y requiere la aprobación explícita o política preautorizada que exige A3 antes de cada acción — este prompt no se autoconcede permiso para ejecutarlo sin esa aprobación
- Detente si: detener y escalar si la reversibilidad de una migración de base de datos no puede confirmarse; detener si no se puede confirmar que la versión previa es desplegable (dependencias, configuración); detener si el rollback implicaría pérdida de datos no aceptada explícitamente por el responsable del si…
- Siguiente: `11-07-sre-postmortem-runbook`

### 11.10 — Capacity planning y proyección de escalamiento
- Archivo: [references/11-10-capacity-planning.md](references/11-10-capacity-planning.md)
- Cuándo usarlo: al planificar un crecimiento esperado (tráfico, volumen de datos, base de usuarios) antes de que ocurra, o después de que `07-06-pruebas-performance-carga` revele un techo de capacidad bajo carga actual que requiere un plan de proyección hacia adelante.
- Entradas: métricas de utilización actual por capa (cómputo, conexiones/almacenamiento de BD, cache, rate limits de APIs de terceros, profundidad de colas), hipótesis de crecimiento esperado y su fuente (proyección de negocio real o supuesto), resultados de pruebas de c…
- Autonomía permitida: A0 — Analizar (lectura de métricas y proyección); A1 — Proponer (plan de escalamiento y umbrales); nunca A2/A3 — este prompt no aprovisiona, redimensiona ni modifica infraestructura
- Detente si: detener y escalar si no hay ninguna métrica de utilización real disponible para el componente crítico — no fabricar cifras plausibles; señalar como proyección de baja confianza si la hipótesis de crecimiento es un supuesto sin respaldo de negocio
- Siguiente: `07-06-pruebas-performance-carga` (skill `sdlc-pruebas`), `11-08-finops-cloud-cost-audit`

### 11.11 — Plan de decomiso de sistema o servicio legacy
- Archivo: [references/11-11-plan-decomiso-sistema-legacy.md](references/11-11-plan-decomiso-sistema-legacy.md)
- Cuándo usarlo: cuando se decide retirar por completo un sistema, servicio o base de datos, antes de ejecutar cualquier acción de apagado.
- Entradas: sistema/servicio a decomisar, inventario conocido de consumidores/integraciones, obligaciones de retención de datos aplicables, fecha objetivo de apagado, disponibilidad de logs de acceso/tráfico reciente al sistema
- Autonomía permitida: A0 — Analizar (inventario de dependientes, obligaciones de retención); A1 — Proponer (plan de comunicación y secuencia de apagado); A3 — Publicar únicamente para ejecutar cada fase de apagado (deshabilitar escritura, pasar a solo lectura, apagado final) contra el sistema real, y solo con aprobación explícita antes de cada fase — no ejecuta ninguna fase de apagado por sí solo
- Detente si: detener si los logs de acceso/tráfico reciente no están disponibles o no cubren un periodo representativo — no asumir que "no hay tráfico visible" significa "no hay dependientes"; detener si existe una obligación de retención de datos sin plan de cumplimiento antes de la fecha de apagado
- Siguiente: `04-05-versionado-deprecacion-api` (skill `sdlc-diseno`), `11-09-runbook-rollback`

### 11.12 — Auditoría de ruido de alertas (alert fatigue)
- Archivo: [references/11-12-auditoria-ruido-alertas.md](references/11-12-auditoria-ruido-alertas.md)
- Cuándo usarlo: cuando el equipo reporta fatiga de alertas (demasiadas notificaciones, alertas ignoradas por costumbre), o periódicamente como salud del sistema de monitoreo ya en producción.
- Entradas: historial de alertas disparadas en el periodo (nombre, timestamp, severidad, si se tomó acción, si se silenció), acceso a dashboards/reglas de alerta actuales, definición de qué constituye "acción tomada" si existe
- Autonomía permitida: A0 — Analizar (clasificación de alertas por ruido/señal); A1 — Proponer (recomendación de tuning, consolidación o eliminación); nunca A2/A3 — la modificación real de reglas de alerta requiere que un humano la aplique tras revisar la recomendación
- Detente si: detener y señalar si el historial de alertas no registra si se tomó acción — no asumir "sin acción visible" como equivalente a "ruido confirmado" sin verificar con el equipo; si el periodo analizado es muy corto para alertas de baja frecuencia, señalar la limitación en vez de concluir que es ruido
- Siguiente: `10-04-observabilidad-instrumentacion` (skill `sdlc-documentacion`), `11-13-salud-rotacion-oncall`

### 11.13 — Auditoría de salud de rotación on-call
- Archivo: [references/11-13-salud-rotacion-oncall.md](references/11-13-salud-rotacion-oncall.md)
- Cuándo usarlo: periódicamente como salud del esquema de guardia, o cuando el equipo reporta fatiga, quejas de inequidad en la rotación, o señales de alta rotación de personal en roles con guardia.
- Entradas: historial de pages/alertas del periodo (quién recibió, timestamp, franja horaria), esquema de rotación configurado (quién está de guardia cuándo), periodo a evaluar, señales cualitativas de burnout o quejas si existen (opcional)
- Autonomía permitida: A0 — Analizar (distribución real de pages, equidad de la rotación); A1 — Proponer (recomendación de rebalanceo); nunca A2/A3 — el cambio real del esquema de guardia requiere decisión y ejecución humana del lead o manager responsable
- Detente si: detener si el historial de pages no distingue horario laboral de nocturno/fin de semana — no asumir que todos los pages tienen el mismo costo de fatiga; detener si el esquema de rotación configurado no está disponible, no inferir turnos a partir del historial de pages únicamente
- Siguiente: `17-04-reporte-capacidad-equipo` (skill `sdlc-backoffice-ingenieria`), `11-12-auditoria-ruido-alertas`

### 11.14 — Plan de migración y cutover de plataforma o sistema legacy
- Archivo: [references/11-14-migracion-cutover-plataforma.md](references/11-14-migracion-cutover-plataforma.md)
- Cuándo usarlo: cuando se decide mover una aplicación, sus datos o su tráfico de un sistema/stack/nube antiguo a uno nuevo (upgrade mayor de stack, migración de nube, consolidación de sistemas, monolito→microservicios) — antes de ejecutar cualquier cutover real, y como paso previo obligatorio a `11-11` si el objetivo final es apagar…
- Entradas: sistema origen y destino (descripción, stack, volumen de datos), arquitectura de destino si existe (`00-D-02`/`04-01`), restricciones de downtime tolerable, dependientes conocidos del sistema origen (inventario de `11-11` si existe)
- Autonomía permitida: A1 — Proponer
- Detente si: si no puede confirmarse una estrategia de verificación de consistencia de datos entre origen y destino, no declarar el plan de cutover como listo para ejecutar — marcarlo como bloqueante en vez de asumir consistencia
- Siguiente: `11-11-plan-decomiso-sistema-legacy`, `11-09-runbook-rollback`

### 11.15 — Plan de recuperación ante desastres y continuidad de negocio (DR/BCP)
- Archivo: [references/11-15-plan-recuperacion-desastres-continuidad.md](references/11-15-plan-recuperacion-desastres-continuidad.md)
- Cuándo usarlo: al definir la arquitectura inicial de un sistema crítico (después de `00-D-02`, donde se declaran los objetivos de RPO/RTO), periódicamente para validar que la capacidad real de recuperación sigue cumpliendo esos objetivos, o al preparar la primera prueba formal de recuperación (drill) de un sistema que nunca ha sido…
- Entradas: objetivos de RTO/RPO declarados (`00-D-02` u otra fuente), arquitectura del sistema y sus dependencias críticas, mecanismo de backup actual (si existe), última prueba de restauración realizada (si alguna)
- Autonomía permitida: A1 — Proponer
- Detente si: si no puede confirmarse que el RTO/RPO objetivo es alcanzable con el mecanismo de backup/replicación actual, no declarar el sistema "recuperable" — marcarlo como brecha de capacidad y reportar el RTO/RPO real estimado en su lugar
- Siguiente: `11-07-sre-postmortem-runbook`, `00-D-04-registro-riesgos-proyecto` (skill `sdlc-fundamentos`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
