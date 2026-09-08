# Deep Interview Context Snapshot: actualizar proyectos

- Timestamp UTC: 20260908T065143Z
- Task statement: actualizar la lista de proyectos del sitio web con la lista bibliográfica/proyecto entregada por el usuario.
- Desired outcome: que la página `/projects/` refleje los 12 proyectos provistos.
- Stated solution: revisar los proyectos actuales del sitio y reemplazar/actualizar el contenido usando la lista entregada.
- Probable intent hypothesis: mantener el portafolio público del laboratorio actualizado con proyectos financiados 2022-2026 y formato académico consistente.
- Prompt-safe initial-context summary status: not_needed.

## Known facts/evidence
[from-code][auto-confirmed]
- Sitio Jekyll/GitHub Pages.
- Página de proyectos: `_pages/projects/index.md`, permalink `/projects/`.
- Datos renderizados desde `_data/projects.yml`.
- El template muestra entradas con `name` + `description`; opcionalmente `photo`, `funding`, `collaborators`, `assignees`.
- Hay 3 proyectos antiguos y una entrada de soporte NVIDIA (`support`) en `_data/projects.yml`.
- No hay AGENTS.md dentro del repo actual; aplica el AGENTS.md proporcionado por el usuario/sesión.
- README describe el laboratorio y áreas de investigación, no define contrato específico para proyectos.


## Constraints
- No implementar dentro de `$deep-interview`; primero cristalizar requerimientos o confirmar handoff.
- Mantener cambios pequeños y verificables.
- No agregar dependencias salvo solicitud explícita.

## Unknowns/open questions
- Si las 12 entradas deben reemplazar solo los proyectos actuales con `name`/`description` o también eliminar/preservar el bloque de soporte NVIDIA.
- Formato deseado: cita completa como descripción, o separar título/financiamiento/autores/institución en campos existentes.
- Idioma/capitalización final deseada.
- Uso de imágenes existentes o dejar sin imágenes.

## Decision-boundary unknowns
- Qué puede decidir OMX sin confirmación sobre estructura YAML/template, soporte NVIDIA, normalización de capitalización y regeneración de `_site`.

## Likely codebase touchpoints
- `_data/projects.yml`
- `_pages/projects/index.md` si se requiere cambiar etiquetas/campos.
- `_site/projects/index.html` si el repo versiona salida generada.

## Relevant repo docs/rules/context inspected
- README.md
- `_pages/projects/index.md`
- `_data/projects.yml`
- `.omx/` (sin context/spec/plans previos relevantes)

## Terminology/doc-code conflicts found
- El sitio usa campos tipo “name/description/funding/collaborators/assignees”; el usuario entregó entradas tipo referencia bibliográfica. Necesita decisión de presentación.
