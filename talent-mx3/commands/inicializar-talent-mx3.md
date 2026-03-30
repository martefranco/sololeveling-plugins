---
description: "Crear estructura de carpetas y ontologia seed"
allowed-tools: Read, Write, Edit, Bash(mkdir:*,cp:*,ls:*), Glob
---

Inicializar la estructura de datos de talent-mx3 en la carpeta de trabajo del usuario.

Este comando se ejecuta una sola vez al empezar a usar el plugin. Crea las carpetas y archivos necesarios para que las skills funcionen.

Pasos:

1. Verificar si ya existe `data/ontologia/` en el directorio de trabajo del usuario.
   - Si ya existe → preguntar: "Ya existe una estructura de talent-mx3 en esta carpeta. ¿Quieres reiniciarla (se perderá lo existente) o solo verificar que esté completa?"
   - Si no existe → continuar con la creación.

2. Crear la estructura de carpetas:
   ```
   data/
   ├── registro.md
   ├── ontologia/
   │   ├── sectores/
   │   │   └── ti-servicios/
   │   │       ├── areas/
   │   │       └── competencias/
   │   │           └── tecnicas/
   │   └── comun/
   │       ├── competencias/
   │       │   ├── conductuales/
   │       │   └── certificaciones/
   │       └── herramientas/
   └── perfiles/
       ├── variaciones/
       └── ofertas/
   ```

3. Copiar los archivos seed desde `${CLAUDE_PLUGIN_ROOT}/data/seed/ontologia/` a `data/ontologia/`.
   Archivos seed incluidos:
   - `indice.md` — Tabla de contenidos de la ontología (con códigos SS-AA)
   - `sectores/ti-servicios/industria.md` — Sector de servicios externalizados
   - `sectores/ti-servicios/areas/atencion-cliente.md` — Roles de atención al cliente
   - `sectores/ti-servicios/areas/operaciones-campo.md` — Roles de campo
   - `sectores/ti-servicios/competencias/tecnicas/soporte-cliente.md` — Competencias técnicas de soporte
   - `sectores/ti-servicios/competencias/tecnicas/campo-telecom.md` — Competencias de telecomunicaciones
   - `comun/competencias/conductuales/catalogo.md` — Competencias conductuales universales
   - `comun/competencias/certificaciones/regulatorias.md` — DC-3, NOM-035, STPS
   - `comun/herramientas/gestion-clientes.md` — CRMs y ticketing
   - `comun/herramientas/gestion-empresarial.md` — ERPs y nómina
   - `comun/herramientas/plataformas.md` — Marketplaces y e-commerce
   - `comun/herramientas/regulatorias.md` — SAT, IMSS, SUA

4. Copiar `${CLAUDE_PLUGIN_ROOT}/data/seed/registro.md` a `data/registro.md`.

5. Presentar resumen:
   "Estructura de talent-mx3 creada. Tienes:
   - Ontología seed con el sector TI/Servicios Externalizados (código 01)
   - Áreas precargadas: Atención al Cliente (01-01) y Operaciones de Campo (01-02)
   - Conocimiento común del mercado mexicano (regulaciones, herramientas, competencias)
   - Registro de códigos SS-AA-PP-VV listo para usar
   - Carpetas de perfiles, variaciones y ofertas listas

   Para empezar: ejecuta /crear-perfil para crear tu primer perfil de puesto.
   Si quieres cargar otra industria: ejecuta /poblar-ontologia."
