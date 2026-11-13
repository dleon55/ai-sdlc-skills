---
name: sdlc-integracion
description: "Prompts AI-SDLC de integración y entrega continua. Úsala cuando trabajes con CI/CD: workflows de GitHub Actions, checklist de promoción entre ambientes, estrategia de feature flags o coordinación de cambios incompatibles (breaking changes)."
license: CC-BY-4.0
---

# Fase AI-SDLC 09 — Integración y entrega continua

Esta skill agrupa los prompts de la fase **Integración y entrega continua** del marco AI-SDLC. Cada prompt está completo en `references/`.

## Cómo usarla

1. Lee primero `references/00-framework.md`: es el contexto obligatorio que antecede a todo prompt.
2. Elige en la lista de abajo el prompt que corresponde a la petición y abre sólo ese archivo de `references/`.
3. Pide al usuario los valores de las variables entre corchetes (`[MODULO]`, `[PEGAR]`, …) que no puedas obtener del repositorio; no las inventes.
4. Respeta la autonomía permitida y detente en cuanto se cumpla un criterio de detención: declara el hueco en lugar de suponer.
5. Al terminar, sugiere el siguiente prompt recomendado.

## Prompts de esta fase

### 9.3 — Revisión de workflows de GitHub Actions
- Archivo: [references/09-03-workflows-github-actions.md](references/09-03-workflows-github-actions.md)
- Cuándo usarlo: periódicamente como revisión de salud del pipeline, o al incorporar nuevos módulos o ambientes.
- Entradas: contenido de `.github/workflows/`, README de CI/CD
- Autonomía permitida: A0 — Analizar
- Detente si: si un workflow referencia secretos o permisos no inspeccionables sin acceso a la configuración del repositorio, documentarlo como brecha de visibilidad en vez de asumir su estado
- Siguiente: `11-02-hardening-seguridad` (skill `sdlc-operaciones`)

### 9.4 — Promotion checklist: integración y despliegue entre ambientes
- Archivo: [references/09-04-promotion-checklist.md](references/09-04-promotion-checklist.md)
- Cuándo usarlo: antes de cualquier despliegue a un ambiente superior, especialmente antes de ir a producción. También útil para definir el proceso estándar de promotion del proyecto.
- Entradas: referencia al issue/PR, rama fuente, ambiente origen y destino, stack de despliegue, indicación de si hay migraciones de BD, cambios de infraestructura o de variables de entorno
- Autonomía permitida: A1 — Proponer (genera el checklist y el semáforo go/no-go; la ejecución del despliegue y del rollback requiere A3 explícito por el responsable de release)
- Detente si: si no hay responsable de rollback disponible, si hay migraciones de BD sin backup confirmado, o si se cumple alguna condición NO-GO explícita del punto 2, detener y no recomendar continuar con el despliegue
- Siguiente: `08-01-revision-completa-pr` (skill `sdlc-revision`)

### 9.5 — Estrategia de feature flags / kill-switch
- Archivo: [references/09-05-estrategia-feature-flags.md](references/09-05-estrategia-feature-flags.md)
- Cuándo usarlo: cuando un cambio necesita un rollout progresivo o controlado en vez de un despliegue de una sola vez — por ejemplo, una feature de alto riesgo, un cambio significativo de UX o un cambio en un flujo crítico de negocio.
- Entradas: feature o cambio a flaggear, tipo de flag esperado (release/ops/experiment), plataforma de feature flags, capas donde se evalúa (cliente/servidor/edge), si hay experimento A/B asociado, fecha u hito objetivo para el rollout completo
- Autonomía permitida: A1 — Proponer (diseño completo de la estrategia sin aplicar); la creación y activación de flags en la plataforma real requiere A2/A3 explícito por el equipo dueño de la feature
- Detente si: detener y escalar si el kill-switch propuesto depende del mismo pipeline de deploy que busca evitar en una emergencia; no proponer una progresión de rollout sin criterios de promoción/pausa medibles; no dejar ningún flag sin propietario ni plan de remoción
- Siguiente: `09-06-coordinacion-breaking-changes`

### 9.6 — Coordinación de breaking changes con equipos externos
- Archivo: [references/09-06-coordinacion-breaking-changes.md](references/09-06-coordinacion-breaking-changes.md)
- Cuándo usarlo: cuando un cambio rompe (o puede romper) un contrato del que dependen otros equipos, servicios o consumidores externos, y hace falta coordinar la comunicación de salida antes de desplegar, no solo el diseño técnico del cambio.
- Entradas: plan de versionado/deprecación ya definido (de `04-05-versionado-deprecacion-api` u otro documento equivalente), lista conocida de equipos/servicios/consumidores que dependen del contrato, fecha objetivo del corte o release, canales de comunicación disponible…
- Autonomía permitida: A1 — Proponer (redacta la comunicación, el calendario de aviso y el checklist de preparación; el envío real de la comunicación, la escalación directa a un consumidor y la decisión de proceder con el corte requieren aprobación humana o del equipo responsable)
- Detente si: detener y escalar si no puede confirmarse la lista completa de consumidores afectados — declararla incompleta en vez de tratarla como cerrada; detener si no hay fecha mínima de aviso definida por audiencia; nunca recomendar proceder con el corte si un consumidor de alto impacto no ha confirmado exp…
- Siguiente: `09-04-promotion-checklist`

---

Adaptado al formato SKILL.md a partir de AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Planes: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills
