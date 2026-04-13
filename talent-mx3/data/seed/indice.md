# Índice de la Ontología — talent-mx3

Tabla de contenidos de la base de conocimiento. Las skills consultan este archivo primero para saber qué existe y dónde encontrarlo.

**Última actualización:** seed inicial

---

## SECTORES

> No hay sectores precargados. Ejecuta `/poblar-ontologia` para construir el conocimiento de tu primera industria.
>
> Los archivos de TI/Servicios Externalizados están disponibles como ejemplo de referencia en `${CLAUDE_PLUGIN_ROOT}/data/seed/sectores/ti-servicios/` — nunca se copian al workspace.

---

## CONOCIMIENTO COMÚN (transversal a todos los sectores)

### Competencias

| Archivo | Contenido | Última actualización |
|---------|-----------|---------------------|
| `comun/competencias/conductuales/catalogo.md` | 15 competencias conductuales universales con definiciones y niveles | seed |
| `comun/competencias/certificaciones/regulatorias.md` | DC-3, DC-4, NOM-035, NOM-009, REPSE, artículos LFT relevantes | seed |

### Herramientas

| Archivo | Contenido | Última actualización |
|---------|-----------|---------------------|
| `comun/herramientas/gestion-clientes.md` | CRMs, ticketing, contact center, helpdesk | seed |
| `comun/herramientas/gestion-empresarial.md` | ERPs, nómina, contabilidad, ofimática | seed |
| `comun/herramientas/plataformas.md` | Marketplaces, e-commerce, plataformas digitales | seed |
| `comun/herramientas/regulatorias.md` | SAT, IMSS, IDSE, SUA, SIPARE, CompraNet | seed |

---

## NOTA

Los códigos SS (sector) y AA (área) se asignan aquí y se replican en `data/registro.md`. Al agregar nuevos sectores o áreas vía `/poblar-ontologia`, actualizar AMBOS archivos.
