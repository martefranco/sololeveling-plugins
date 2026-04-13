# Registro Central de Códigos — talent-mx3

Tabla maestra de asignación de códigos SS-AA-PP-VV. Consultar SIEMPRE antes de crear un sector, área, perfil o variación.

**Última actualización:** seed inicial

---

## Convención de códigos

| Nivel | Formato | Ejemplo |
|-------|---------|---------|
| Sector (SS) | 2 dígitos | `01` = TI / Servicios Externalizados |
| Área (AA) | 2 dígitos dentro del sector | `01` = Atención al Cliente |
| Perfil Core (PP) | 2 dígitos dentro del área | `01` = Asesor de Soporte N1 |
| Variación (VV) | 2 dígitos dentro del perfil | `01` = Proyecto Teams - Transf. Digital |

**Nomenclatura de archivos (v4.0.0):**

Los códigos SS y AA dan contexto a través de la ruta del directorio, no del nombre de archivo. Solo PP y VV aparecen en el nombre del archivo.

- Perfil Core: `PP-titulo-slug.md` → `01-asesor-soporte-n1.md`
  - Ruta: `data/sectores/<sector>/areas/<area>/perfiles/`
- Variación: `PP-VV-titulo-slug--contexto.md` → `01-01-asesor-soporte-n1--proyecto-teams.md`
  - Ruta: `data/sectores/<sector>/areas/<area>/perfiles/variaciones/`
- Oferta: `PP-VV-titulo-slug--plataforma.md` → `01-01-asesor-soporte-n1--linkedin.md`
  - Ruta: `data/sectores/<sector>/areas/<area>/perfiles/ofertas/`

---

## SECTORES (SS)

| Código | Slug ontología | Nombre | Fecha |
|--------|---------------|--------|-------|
| — | — | (sin sectores registrados) | — |

---

## ÁREAS (SS-AA)

| Código | Sector | Slug ontología | Nombre | Fecha |
|--------|--------|---------------|--------|-------|
| — | — | — | (sin áreas registradas) | — |

---

## PERFILES CORE (SS-AA-PP)

| Código | Área | Archivo | Título del perfil | Fecha |
|--------|------|---------|-------------------|-------|
| — | — | — | (sin perfiles creados aún) | — |

---

## VARIACIONES (SS-AA-PP-VV)

| Código | Perfil Core | Archivo | Contexto de variación | Fecha |
|--------|------------|---------|----------------------|-------|
| — | — | — | (sin variaciones creadas aún) | — |
