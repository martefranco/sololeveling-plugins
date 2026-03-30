# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. Plugins are tool-agnostic — they describe workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category | Placeholder | Options |
|----------|-------------|---------|
| Git/Version Control | `~~git` | GitHub, GitLab, Bitbucket |

## Notes

talent-mx3 uses `~~git` for sincronizar la ontología (`data/ontologia/`) con un repositorio remoto. Esto permite que el conocimiento persista entre sesiones y se comparta entre usuarios.

La conexión a `~~git` es **opcional** — el plugin funciona sin ella, pero sin persistencia remota la ontología solo existe localmente.
