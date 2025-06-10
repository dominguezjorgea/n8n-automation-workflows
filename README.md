# n8n-automation-workflows

Collection of automation workflows built with n8n, including AI agents, business automation, and integrations.

# 🧠 n8n Automation Workflows – MCP Integration Guide

This repository contains automation workflows built with [n8n](https://n8n.io/), focusing on the integration of AI agents through MCP (Model Context Protocol). Below is a step-by-step guide on how to configure **community MCP nodes**, environment variables, and client credentials for GitHub and Firecrawl MCP servers.

> ⚠️ **Note:** Community nodes are only supported in **self-hosted n8n instances**, not in the cloud version.

---

## 🚀 1. Configure Custom MCP Nodes in Self-hosted n8n

1. Ensure your instance of n8n is **self-hosted**.
2. Keep your n8n instance **updated** to access the latest community nodes.
3. Go to your profile → `Settings` → `Community nodes`.
4. Click `Browse` and search for nodes related to **MCP** (e.g., `N8N Note MCP` or similar).
5. Copy the node name and return to settings to **install** it.
6. If already installed, you'll receive a notification.
7. After installation, ensure the node is up to date.

---

## 🛠️ 2. Enable Environment Variable to Use Community Nodes as Tools

To use MCP nodes as **tools** for AI agents:

1. Add the following environment variable to your Docker or VPS setup:

   ```env
   N8N_COMMUNITY_PACKAGE_ALLOW="packageName1, packageName2"
   ```

## 3. Configuración del Cliente MCP para GitHub

Para conectar tu agente de IA en N8N a un servidor MCP de GitHub, necesitas configurar una credencial con tu token de acceso personal de GitHub. [5]

1.  En N8N, ve a **Credenciales** y crea una nueva credencial. [5]
2.  Selecciona el tipo de credencial que corresponde al nodo MCP que instalaste (probablemente se llame "MCP Credencial" o similar). [5]
3.  Configura los siguientes campos: [5]
    - **Command:** `mpx -y` [5]
    - **Arguments:** `github-mcp` [5]
    - **Environment Variables:** Aquí añadirás tu token de GitHub. La variable se llama `GITHUB_PERSONAL_ACCESS_TOKEN`. [3, 5]
      - **Cómo obtener tu `GITHUB_PERSONAL_ACCESS_TOKEN`:** [5]
        - Ve a tu cuenta de GitHub en la web. [5]
        - Haz clic en tu perfil y luego en `Settings`. [5]
        - En el menú lateral, selecciona `Developer settings`. [5]
        - Haz clic en `Personal access tokens`. [5]
        - Selecciona **`Tokens (classic)`**. [5]
        - Haz clic en `Generate new token` y luego en `Generate new token (classic)`. [5]
        - Asígnale un nombre descriptivo. [5]
        - Establece una **expiración** para el token (por seguridad, no selecciones "No expiration" a menos que sea estrictamente necesario). Por ejemplo, 7 días. [5]
        - **Selecciona los permisos (scopes)** necesarios. Esto es crucial y debe alinearse con las capacidades del servidor MCP de GitHub. Para acciones comunes, necesitas permisos como acceder a `commits`, `public repos`, `invitations`, **`read and write` en `workflows`**, `write package`, y potencialmente algunos permisos de `admin.org`. [3] **Sé extremadamente cuidadoso con los permisos de administración**, ya que un agente podría borrar repositorios o incluso tu cuenta si tiene permisos amplios. [3]
        - Haz clic en `Generate token`. [3]
        - **Copia el token generado inmediatamente**. Una vez que abandones la página, no podrás verlo de nuevo. [3]
      - Regresa a N8N y en el campo `Environment Variables`, añade tu token con la sintaxis: `GITHUB_PERSONAL_ACCESS_TOKEN=TU_TOKEN_COPIADO_AQUI`. [5]
4.  Haz clic en **Guardar** la credencial. [3]

¡Listo! Ya tienes una credencial MCP configurada para GitHub, permitiendo a tus agentes de IA realizar acciones como crear, actualizar o buscar repositorios, gestionar pull requests, etc. [5, 6]

## 4. Configuración del Cliente MCP para Firecrawl

Para conectar tu agente de IA en N8N a un servidor MCP de Firecrawl (un servicio para web scraping), necesitas configurar una credencial con tu API Key de Firecrawl. [3]

1.  En N8N, ve a **Credenciales** y crea una nueva credencial. [5]
2.  Selecciona el tipo de credencial MCP. [5]
3.  Configura los siguientes campos: [5]
    - **Command:** `mpx -y` [3]
    - **Arguments:** `firecrawl-mcp` [3]
    - **Environment Variables:** Aquí añadirás tu API Key de Firecrawl. [7]
      - **Cómo obtener tu Firecrawl API Key:**
        - Ve al sitio web de Firecrawl e inicia sesión en tu cuenta. [7]
        - Tu API Key estará visible en tu dashboard o configuración de cuenta para que la copies. [7]
      - Regresa a N8N y en el campo `Environment Variables`, añade tu API Key. La sintaxis es `NOMBRE_VARIABLE_FIRECRAWL=TU_API_KEY_COPIADA_AQUI`. (Nota: El nombre exacto de la variable de entorno para la API Key de Firecrawl no se especifica en los fuentes proporcionados, pero sigue el patrón `NOMBRE_SERVICIO_API_KEY`. Deberías verificar el nombre exacto si encuentras documentación específica para el servidor Firecrawl MCP que estás usando, aunque el patrón `FIRECRAWL_API_KEY` es común). [7]
4.  Haz clic en **Guardar** la credencial.

¡Hecho! Ahora puedes usar la credencial de Firecrawl MCP para que tus agentes de IA interactúen con este servicio, realizando acciones como `scrape` (extraer contenido de una página web) o `map` (descubrir URLs desde un punto de partida). [8]
