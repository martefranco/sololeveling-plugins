# Reglas de Nomenclatura SS-AA-PP-VV

## Sistema de códigos

El sistema usa 4 niveles jerárquicos con 2 dígitos cada uno:

```
SS  - Sector       (01-99)
AA  - Área          (01-99 por sector)
PP  - Perfil Core   (01-99 por área)
VV  - Variación     (01-99 por perfil)
```

## Reglas de asignación

### Al crear cualquier elemento:
1. SIEMPRE leer `data/registro.md` antes de asignar un código
2. Usar el siguiente número disponible en la secuencia
3. Registrar inmediatamente en `data/registro.md` después de crear
4. NUNCA reutilizar un código, incluso si el elemento fue eliminado

### Nomenclatura de archivos

**Perfil Core:**
```
SS-AA-PP-titulo-slug.md
```
Ejemplo: `01-03-01-especialista-ia-llm.md`

**Variación:**
```
SS-AA-PP-VV-titulo-slug--contexto-slug.md
```
Ejemplo: `01-03-01-01-especialista-ia-llm--transf-digital.md`

**Oferta (generada desde variación):**
```
SS-AA-PP-VV-titulo-slug--plataforma.md
```
Ejemplo: `01-03-01-01-especialista-ia-llm--linkedin.md`

**Oferta (generada desde Core, sin variación):**
```
SS-AA-PP-00-titulo-slug--plataforma.md
```
Ejemplo: `01-03-01-00-especialista-ia-llm--linkedin.md`

### Reglas del slug
- Solo minúsculas, sin acentos
- Separar palabras con guion `-`
- Separar contexto/plataforma con doble guion `--`
- Máximo 50 caracteres en el slug (sin contar código ni separadores)

## Mapeo con ontología

Los códigos de sector (SS) y área (AA) se corresponden con la estructura de la ontología:

| Código SS | Carpeta ontología |
|-----------|-------------------|
| 01 | `sectores/ti-servicios/` |

| Código SS-AA | Archivo ontología |
|-------------|-------------------|
| 01-01 | `sectores/ti-servicios/areas/atencion-cliente.md` |
| 01-02 | `sectores/ti-servicios/areas/operaciones-campo.md` |

Este mapeo se mantiene en `data/registro.md` y en `data/ontologia/indice.md`.

## Cuándo se asigna cada código

| Momento | Quién asigna | Qué se registra |
|---------|-------------|-----------------|
| `/poblar-ontologia` o `/inicializar-talent-mx3` | constructor-ontologia | SS y AA |
| `/crear-perfil` | constructor-perfil | PP (y opcionalmente VV si el Intake genera variación) |
| `/crear-variacion` | constructor-perfil (modo 2) | VV |

## Flujo de consulta

```
¿Necesito crear un perfil?
  → Leer data/registro.md
  → ¿El sector ya tiene código SS?
      SÍ → usar ese código
      NO → asignar siguiente SS, registrar
  → ¿El área ya tiene código AA?
      SÍ → usar ese código
      NO → asignar siguiente AA, registrar
  → Asignar siguiente PP disponible en ese SS-AA
  → Registrar en data/registro.md
  → Guardar archivo con nombre SS-AA-PP-slug.md
```
