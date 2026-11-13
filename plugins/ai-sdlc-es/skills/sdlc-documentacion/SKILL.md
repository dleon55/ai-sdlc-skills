---
name: sdlc-documentacion
description: "Prompts AI-SDLC de documentación. Úsala cuando haya que documentar: documentación técnica, memoria técnica del proyecto, notas de versión y CHANGELOG, observabilidad e instrumentación, documentación de API pública o materiales de capacitación para el despliegue."
license: CC-BY-4.0
---

# Fase AI-SDLC 10 — Documentación

Esta skill agrupa los prompts de la fase **Documentación** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 10.1 — Actualizar documentación técnica
- Archivo: [references/10-01-documentacion-tecnica.md](references/10-01-documentacion-tecnica.md)
- Cuándo usarlo: al cierre de cada cambio, antes de hacer merge a la rama principal.
- Entradas: issue o requerimiento de referencia, rama integrada, componentes modificados, documentos existentes a revisar (README, docs/, arquitectura, contratos API)
- Autonomía permitida: A1 — Proponer: entrega lista de documentos a actualizar con contenido propuesto, sin aplicar el cambio
- Detente si: si el cambio real o los componentes modificados no están claros, debe solicitar esa información antes de proponer contenido inventado
- Siguiente: `10-02-memoria-tecnica`, `10-03-release-changelog`

### 10.2 — Memoria técnica del cambio
- Archivo: [references/10-02-memoria-tecnica.md](references/10-02-memoria-tecnica.md)
- Cuándo usarlo: al cierre de cada issue o sprint, como registro formal del trabajo realizado para auditoría y referencia futura.
- Entradas: issue o requerimiento, rama integrada, ambiente, componentes modificados, commits/PRs, diseño aprobado, resultados de pruebas ejecutadas
- Autonomía permitida: A1 — Proponer: redacta el documento de memoria técnica; no lo publica ni archiva por sí mismo
- Detente si: si faltan resultados de pruebas o el diseño aprobado no está disponible, debe señalarlo explícitamente en la sección correspondiente en vez de inventar resultados
- Siguiente: `10-03-release-changelog`, `11-03-deuda-tecnica` (skill `sdlc-operaciones`)

### 10.3 — Documentación de release o changelog
- Archivo: [references/10-03-release-changelog.md](references/10-03-release-changelog.md)
- Cuándo usarlo: al preparar un release o al cerrar un sprint para documentar cambios entregados.
- Entradas: versión o tag, rama de release, issues o PRs incluidos, commits del período
- Autonomía permitida: A1 — Proponer: entrega el changelog listo para publicar; la publicación efectiva en GitHub Releases o CHANGELOG.md es una acción A3 separada y explícita
- Detente si: si detecta cambios que rompen compatibilidad sin nota de migración clara, debe detenerse y solicitar esa información antes de dar el changelog por completo
- Siguiente: `10-02-memoria-tecnica`, `09-04-promotion-checklist` (skill `sdlc-integracion`)

### 10.4 — Observabilidad: Instrumentación y Monitoreo
- Archivo: [references/10-04-observabilidad-instrumentacion.md](references/10-04-observabilidad-instrumentacion.md)
- Cuándo usarlo: al incorporar observabilidad a un sistema nuevo, al revisar la cobertura de monitoreo antes de un despliegue mayor, o cuando se identifican puntos ciegos en la detección de fallos en producción.
- Entradas: stack tecnológico, infraestructura, stack de observabilidad actual, número de servicios, SLAs comprometidos con clientes, entorno objetivo; opcionalmente resultado de `13-04` (threat modeling)
- Autonomía permitida: A1 — Proponer: catálogo de SLOs, alertas y dashboards; la instrumentación real en código y el despliegue de agentes/exporters requiere A2 en workspace o rama aislada con revisión posterior
- Detente si: si no hay SLAs ni objetivos de negocio definidos para fijar los SLOs, debe señalarlo en vez de inventar umbrales; no debe proponer instrumentación que loguee contraseñas, tokens o PII sin anonimizar
- Siguiente: `11-05-performance-produccion-diagnostico` (skill `sdlc-operaciones`), `11-04-incident-response` (skill `sdlc-operaciones`)

### 10.5 — Documentación pública de API para desarrolladores externos
- Archivo: [references/10-05-documentacion-api-publica.md](references/10-05-documentacion-api-publica.md)
- Cuándo usarlo: después de que el contrato de API ya está diseñado (`04-06`) e implementado, antes de exponerlo a consumidores externos (partners, clientes, terceros).
- Entradas: contrato de API ya implementado (referencia a `04-06` o especificación real), audiencia objetivo (desarrolladores externos/partners/clientes), ejemplos de uso reales si existen
- Autonomía permitida: A1 — Proponer
- Detente si: si el comportamiento a documentar no puede verificarse contra la implementación real (el contrato de diseño quedó desactualizado respecto al código), detente y señala la discrepancia en vez de documentar el diseño teórico como si fuera el comportamiento real
- Siguiente: `10-03-release-changelog`

### 10.6 — Materiales de capacitación y plan de rollout para usuarios finales
- Archivo: [references/10-06-materiales-capacitacion-rollout.md](references/10-06-materiales-capacitacion-rollout.md)
- Cuándo usarlo: antes de lanzar una funcionalidad o sistema nuevo a sus usuarios finales no técnicos, especialmente si implica un cambio de flujo de trabajo existente o afecta a un grupo grande de usuarios.
- Entradas: descripción de la funcionalidad o sistema a lanzar, audiencia de usuarios finales (roles, nivel técnico, tamaño del grupo), canal de comunicación disponible, fecha de lanzamiento
- Autonomía permitida: A1 — Proponer
- Detente si: si no se conoce el nivel técnico o el tamaño de la audiencia, detente y solicítalo antes de proponer el formato de capacitación — un video corto y una guía escrita no sirven igual para 5 usuarios expertos que para 500 usuarios no técnicos
- Siguiente: `17-06-reporte-estado-stakeholders` (skill `sdlc-backoffice-ingenieria`)

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
