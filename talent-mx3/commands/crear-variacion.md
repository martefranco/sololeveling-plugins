---
description: "Derivar variacion de un perfil existente"
allowed-tools: Read, Write, Edit, Glob, Grep
argument-hint: "<nombre-del-perfil-core>"
---

Crear una Variación a partir de un Perfil Core existente.

Lee la sección "MODO 2: Crear Variación" de `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/SKILL.md`.

Pasos:
1. Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/reglas-nomenclatura.md` para el sistema de códigos.
2. Leer `data/registro.md` para conocer los códigos ya asignados.
3. Si el usuario proporcionó argumento `$ARGUMENTS`, buscar el perfil core en `data/perfiles/` que coincida.
4. Si no proporcionó argumento, listar los perfiles disponibles en `data/perfiles/` (excluyendo subcarpetas) y pedir que elija uno.
5. Cargar el Perfil Core seleccionado.
6. Presentar resumen de lo que se hereda: competencias técnicas, conductuales, herramientas, must-haves.
7. Preguntar contexto de la variación: "¿Para qué cliente, proyecto o especialidad es esta variación?"
8. Recopilar: contexto de negocio, ubicación organizacional, equipo/microcultura, métricas de éxito, competencias adicionales, condiciones/salario.
9. Generar la Variación con el formato de `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/formato-perfil-core.md` (sección Variación, 6 secciones).
10. Asignar código VV (siguiente disponible para ese SS-AA-PP) y registrar en `data/registro.md`.
11. Validar con `${CLAUDE_PLUGIN_ROOT}/skills/validador-legal-mx/references/catalogo-reglas.md`.
12. Guardar en `data/perfiles/variaciones/SS-AA-PP-VV-titulo-slug--contexto.md`.

La variación debe mantener coherencia con el Core. Si el usuario quiere cambiar algo que es del Core, preguntar: "Esto cambiaría el perfil base que es reutilizable. ¿Quieres actualizar el Core o solo ajustarlo para esta variación?"
