# Registro MCP autorizado (GitHub Copilot)

Registro MCP v0.1 estático que actúa como **lista blanca** de servidores MCP para
GitHub Copilot Business en la organización (política **Registry only**).

Se despliega automáticamente en **Azure Static Web Apps (plan Free)** con cada cambio en `main`.

## Servidores autorizados

| Servidor | ID en el registro | URL | Ficha |
|---|---|---|---|
| Figma (remoto) | `com.nunsys.figma/mcp` | `https://mcp.figma.com/mcp` | `figma.json` |
| Azure DevOps (remoto) | `com.nunsys.azuredevops/mcp` | `https://mcp.dev.azure.com/nunsysSW` | `azure-devops.json` |

## Ficheros

| Fichero | Función |
|---|---|
| `servers.json` | Respuesta de `GET /v0.1/servers` (lista de todos los servidores) |
| `<servidor>.json` | Ficha de cada servidor (`/v0.1/servers/{name}/versions/...`) |
| `staticwebapp.config.json` | Rutas `/v0.1/...` y cabeceras CORS |
| `index.html` | Página raíz (obligatoria en Static Web Apps) |

## Añadir un servidor nuevo

1. Crear `<servidor>.json` con la ficha (copiar uno existente). El `name` debe tener
   un prefijo único, p. ej. `com.nunsys.<servidor>/mcp`.
2. Añadir la misma ficha a la lista de `servers.json` y actualizar `metadata.count`.
3. Añadir una ruta en `staticwebapp.config.json`:
   `{ "route": "/v0.1/servers/com.nunsys.<servidor>*", "rewrite": "/<servidor>.json" }`
4. Actualizar la tabla de este README.

## Cómo proponer un cambio

1. Crea una rama y modifica los ficheros.
2. Abre un Pull Request contra `main`.
3. Otro miembro del equipo `mcp-registry-admins` debe aprobarlo.
4. Al fusionar, el GitHub Action despliega el registro y Copilot aplica la nueva lista.

## Gestión del equipo

- Los miembros del equipo `mcp-registry-admins` tienen rol **Admin** en este repositorio.
- Los *maintainers* del equipo pueden añadir o quitar miembros (deben ser miembros de la organización).
