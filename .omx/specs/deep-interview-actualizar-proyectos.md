# Execution Spec: actualizar proyectos del sitio

## Metadata
- Source workflow: `$deep-interview`
- Profile: standard
- Rounds: 2
- Final ambiguity: 5%
- Threshold: 20%
- Context type: brownfield
- Context snapshot: `.omx/context/actualizar-proyectos-20260908T065143Z.md`
- Transcript: `.omx/interviews/actualizar-proyectos-20260908T065644Z.md`

## Intent
Actualizar la página pública de proyectos del sitio para que refleje la lista vigente de 12 proyectos entregada por el usuario, eliminando contenido anterior que ya no debe aparecer en esa sección.

## Desired outcome
La página `/projects/` debe mostrar únicamente los 12 proyectos proporcionados por el usuario, usando la plantilla actual del sitio.

## In scope
- Reemplazar todas las entradas actuales de proyectos en `_data/projects.yml` por las 12 entradas nuevas.
- Eliminar también el bloque actual de soporte NVIDIA de `_data/projects.yml` porque el usuario eligió `replace-all`.
- Mantener `_pages/projects/index.md` sin rediseño si la plantilla actual puede renderizar correctamente los nuevos datos.
- Usar una entrada por proyecto:
  - `name`: título del proyecto.
  - `funding`: instrumento y número, por ejemplo `FONDECYT REGULAR No. 1241915`.
  - `collaborators`: autores/investigadores de la entrada provista.
  - `description`: año e institución cuando esté disponible; si no hay institución, solo año o una frase breve basada en la cita.
  - `photo`: omitir salvo que el usuario entregue imágenes nuevas.
- Preservar caracteres españoles y acentos en UTF-8.

## Out of scope / Non-goals
- No conservar los 3 proyectos antiguos.
- No conservar el bloque NVIDIA en la sección de proyectos.
- No agregar imágenes nuevas ni reutilizar imágenes antiguas sin indicación explícita.
- No cambiar el diseño visual ni crear una nueva plantilla si la actual funciona.
- No agregar dependencias.
- No inventar instituciones faltantes.

## Decision boundaries
OMX puede decidir sin nueva confirmación:
- Normalizar YAML para que Jekyll lo renderice de forma segura.
- Ajustar puntuación menor requerida por YAML/HTML, sin cambiar nombres, títulos, años, fondos o instituciones.
- Dejar campos opcionales ausentes cuando no exista dato en la lista del usuario.
- Ejecutar build/verificación local.

OMX debe pedir confirmación antes de:
- Cambiar sustantivamente títulos, autores, años, números de proyecto o instituciones.
- Traducir títulos entre inglés/español.
- Agregar imágenes o rediseñar la página.
- Publicar/deployar fuera del flujo normal de GitHub Pages local/repo.

## Constraints
- Brownfield Jekyll/GitHub Pages.
- Fuente renderizada actual: `_data/projects.yml`.
- Template actual: `_pages/projects/index.md` muestra `name`, `photo`, `funding`, `collaborators`, `assignees`, `description`; entradas con `support` se renderizan en un bloque separado.
- Mantener cambios pequeños y reversibles.

## Testable acceptance criteria
1. `_data/projects.yml` contiene exactamente 12 entradas de proyecto con `name` y no contiene entradas `support`.
2. Los 12 títulos de la lista del usuario aparecen en el sitio renderizado o en el YAML fuente.
3. No aparecen los títulos antiguos de DLBCL/transporter ni el bloque NVIDIA en `/projects/`.
4. El sitio Jekyll compila localmente sin errores.
5. La página `/projects/` conserva la plantilla actual y renderiza cada proyecto con título, funding, collaborators y descripción cuando corresponda.

## Assumptions exposed + resolutions
- Assumption: “actualizar a esta lista” podía significar reemplazar, anexar o reemplazar solo proyectos. Resolution: usuario eligió reemplazar todo.
- Assumption: la lista podía requerir rediseño bibliográfico. Resolution: usuario eligió mantener plantilla actual.

## Pressure-pass findings
Round 2 presionó la decisión de Round 1: reemplazar todo no implica rediseñar. La resolución fue reemplazo completo de datos con plantilla existente.

## Brownfield evidence vs inference
[from-code][auto-confirmed]
- `_pages/projects/index.md` itera sobre `site.data.projects`.
- Las tarjetas de proyecto requieren `project.name` y `project.description`.
- `_data/projects.yml` contiene actualmente 3 entradas con `name` y una entrada `support` NVIDIA.

[from-user]
- Reemplazar todo.
- Mantener plantilla actual.

## Docs/Terminology ledger
- Inspected: `README.md`, `_pages/projects/index.md`, `_data/projects.yml`, `.omx/` state/context availability.
- No repo-local `AGENTS.md` found.
- Term conflict resolved: user’s bibliographic entries will be adapted to the existing “Projects” template rather than converted into a new bibliography template.

## Project entries to implement
- **2024 — Identification Of New Chemical Biomarkers Associated With Molecular Subtypes Of Gastric Cancer Embedded Tissue Of Chilean Patients, Using Untargeted Metabolomics And Spatialomics Analytical Approach**; Authors: Bustamante Salazar, L. A.; Mardones Peña, C.; Pérez de Armas, A. J.; Delgado Schneider, C. P.; Salas Burgos, A.; Funding: FONDECYT REGULAR No. 1241915; Institution: Universidad de Concepción.
- **2024 — Despliegue Territorial De Hoja De Ruta Para La Aceleración Del Impacto Sostenible De La Ciencia, Tecnología, Conocimiento E Innovación A Través Del Desarrollo De Consorcios De Investigación**; Authors: Cabezas, M.; Muñoz, G.; Salas Burgos, A.; Funding: NODO ANID No. NODO240003; Institution: Universidad de Concepción.
- **2026 — CTCI Para El Desarrollo De Futuros Territoriales Sostenibles**; Authors: Cabezas, M.; Salas Burgos, A.; Funding: NMC ANID No. NMCA250001; Institution: Universidad de Concepción.
- **2024 — Unraveling The Covalent Binding Mechanism Of Telomerase To Guide The Search For Effective Cancer Inhibitors**; Authors: Jaña Villalobos, G. A.; Uribe Pérez, E. A.; Salas Burgos, A.; Funding: FONDECYT REGULAR No. 1241355; Institution: Universidad Andrés Bello.
- **2024 — Caracterización Del Efecto Del Orden Temporal De Mutaciones Impulsoras En El Gen Tp53 En La Heterogeneidad Intratumoral Desde Biopsias De Pacientes Con Cáncer Gástrico**; Authors: Muñoz Maulen, D.; Salas Burgos, A.; Funding: FONDECYT POSTDOC No. FONDECYT3240234; Institution: Universidad de Concepción.
- **2022 — Caracterización Estructural De Complejos Proteicos Involucrados En Fibrodisplasia Osificante Progresiva (FOP): Desarrollo De Un Modelo Reportero Para Acelerar El Diseño De Una Terapia Específica**; Authors: Quevedo Langenegger, E. I.; Salas Burgos, A.; Araya Secchi, R.; Funding: VRID - MULTIDISCIPLINARIA No. 2021000357MUL.
- **2024 — Iscan Integrated Platform: A Friendly, Versatile, And Cost-efficient Mass Genotyping Tool For Global Genetic Characterization At A Population Scale**; Authors: Ramires, R.; Salas Burgos, A.; Funding: FONDEQUIP MAYOR No. EQY220014; Institution: Universidad de Concepción.
- **2022 — Towards systems pharmacology to design multi-target directed ligands as therapeutic alternatives for Alzheimer’s disease.**; Authors: Ramírez Sánchez, D.; Salas Burgos, A.; Funding: FONDECYT No. 1220656.
- **2023 — Nodo CTCI-MCS: Consolidación de la institucionalidad del Nodo CTCI Macrozonal Centro Sur para la Aceleración del Impacto Territorial de la Ciencia Abierta**; Authors: Salas Burgos, A.; Funding: ANID No. NODO220006.
- **2023 — Euca-drought: ¿plataforma De Selección De Variedades De Eucalyptus Sp. Tolerantes A Sequía Y De Mayor Eficiencia De Uso De Agua**; Authors: Ulloa Fuentes, J. L.; Hasbun Zaror, R.; Rubilar Pons, R.; Castillo Felices, R.; Salas Burgos, A.; Funding: ID23I10390.
- **2026 — Evaluating The Role Of Macrophage Epigenetic Wiring In Cancer Aging**; Authors: Villagra Macaya, A.; Hepp Castro, M.; Salas Burgos, A.; Funding: FONDECYT REGULAR No. 1260559; Institution: Universidad Católica de la Santísima Concepción.
- **2026 — Interdisciplinary Approach To Breast Cancer In A Rural/agricultural Context: Integrating Environmental, Biological, And Social Determinants In The Maule Region**; Authors: Zúñiga Venegas, L.; Landeros, N.; Salas Burgos, A.; Funding: FONDECYT REGULAR No. 1262233; Institution: Universidad Católica de la Santísima Concepción.

## Recommended handoff
Default: `$ultragoal create-goals --brief-file .omx/specs/deep-interview-actualizar-proyectos.md` then complete goals.
For this small scoped update, direct execution from this spec is low-risk if the user selects/permits an execution handoff.
