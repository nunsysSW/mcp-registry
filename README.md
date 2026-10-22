# Registro MCP autorizado (GitHub Copilot)

Registro MCP v0.1 estático que actúa como **lista blanca** de servidores MCP para
GitHub Copilot Business en la organización (política **Registry only**).

Se despliega automáticamente en **Azure Static Web Apps (plan Free)** con cada cambio en `main`.

## Servidores autorizados

| Servidor | ID en el registro | URL |
|---|---|---|
| Figma (remoto) | `com.nunsys/figma` | `https://mcp.figma.com/mcp` |

## Ficheros

| Fichero | Función |
|---|---|
| `servers.json` | Respuesta de `GET /v0.1/servers` |
| `server.json` | Respuesta de `GET /v0.1/servers/{name}/versions/latest` y `/versions/{version}` |
| `staticwebapp.config.json` | Rutas `/v0.1/...` y cabeceras CORS |

## Cómo proponer un cambio

1. Crea una rama y modifica los ficheros.
2. Abre un Pull Request contra `main`.
3. Otro miembro del equipo `mcp-registry-admins` debe aprobarlo.
4. Al fusionar, el GitHub Action despliega el registro y Copilot aplica la nueva lista.

## Gestión del equipo

- Los miembros del equipo `mcp-registry-admins` tienen rol **Admin** en este repositorio.
- Los *maintainers* del equipo pueden añadir o quitar miembros (deben ser miembros de la organización).
