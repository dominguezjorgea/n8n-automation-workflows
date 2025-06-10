---
## 🚀 Configuring the MCP Client environment

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

## Configuring the MCP Client for GitHub

To connect your AI agent in N8N to an MCP GitHub server, you need to configure a credential with your GitHub personal access token.

1.  In N8N, go to **Credentials** and create a new credential.
2.  Select the credential type corresponding to the MCP node you installed (likely named "MCP Credential" or similar).
3.  Configure the following fields:
    - **Command:** `mpx -y`
    - **Arguments:** `github-mcp`
    - **Environment Variables:** Here you will add your GitHub token. The variable is named `GITHUB_PERSONAL_ACCESS_TOKEN`.
      - **How to get your `GITHUB_PERSONAL_ACCESS_TOKEN`:**
        - Go to your GitHub account on the web.
        - Click on your profile and then on `Settings`.
        - In the side menu, select `Developer settings`.
        - Click on `Personal access tokens`.
        - Select **`Tokens (classic)`**.
        - Click on `Generate new token` and then on `Generate new token (classic)`.
        - Give it a descriptive name.
        - Set an **expiration** for the token (for security, do not select "No expiration" unless strictly necessary). For example, 7 days.
        - **Select the necessary permissions (scopes)** [2, 4]. This is crucial and must align with the capabilities of the GitHub MCP server. For common actions, you need permissions such as accessing `commits`, `public repos`, `invitations`, **`read and write` on `workflows`**, `write package`, and potentially some `admin.org` permissions. **Be extremely careful with administration permissions**, as an agent could delete repositories or even your account if it has broad permissions.
        - Click on `Generate token`.
        - **Copy the generated token immediately** [2]. Once you leave the page, you won't be able to see it again.
      - Return to N8N and in the `Environment Variables` field, add your token with the syntax: `GITHUB_PERSONAL_ACCESS_TOKEN=YOUR_COPIED_TOKEN_HERE`.
4.  Click **Save** the credential.

Done! You now have an MCP credential configured for GitHub, allowing your AI agents to perform actions like creating, updating, or searching repositories, managing pull requests, etc.

## Configuring the MCP Client for Firecrawl

To connect your AI agent in N8N to an MCP Firecrawl server (a web scraping service), you need to configure a credential with your Firecrawl API Key [2, 6].

1.  In N8N, go to **Credentials** and create a new credential [4].
2.  Select the MCP credential type [4].
3.  Configure the following fields:
    - **Command:** `mpx -y` [2]
    - **Arguments:** `firecrawl-mcp` [2]
    - **Environment Variables:** Here you will add your Firecrawl API Key [2, 6].
      - **How to get your Firecrawl API Key:**
        - Go to the Firecrawl website and log into your account [6].
        - Your API Key will be visible on your dashboard or account settings for you to copy [6].
      - Return to N8N and in the `Environment Variables` field, add your API Key [6]. The syntax is `YOUR_FIRECRAWL_VARIABLE_NAME=YOUR_COPIED_API_KEY_HERE` [2, 6]. (Note: The exact name of the environment variable for the Firecrawl API Key is not specified in the provided sources, but it follows the pattern `SERVICE_NAME_API_KEY`. You should verify the exact name if you find specific documentation for the Firecrawl MCP server you are using, although the pattern `FIRECRAWL_API_KEY` is common).
4.  Click **Save** the credential [2].

Finished! Now you can use the Firecrawl MCP credential for your AI agents to interact with this service, performing actions like `scrape` (extracting content from a web page) or `map` (discovering URLs from a starting point) [7].

_(Optional):_ The sources mention that you can connect to Firecrawl (and other) MCP servers through marketplaces like Smitery [3, 8, 9]. In this case, the `mpx` command and arguments might be provided by the marketplace, and they will typically still require your Firecrawl API Key in the environment variables [6].

## Using MCP Clients in N8N Workflows

Once the credentials are configured, you can use the **MCP Client** node in your N8N workflows [10]. This node will allow you to:

1.  Select the MCP credential you created for GitHub or Firecrawl [10].
2.  Choose an **operation**:
    - `list tools`: For the AI agent (or you) to discover the capabilities (`tools`) that the MCP server exposes [10].
    - `execute tool`: For the agent to execute a specific capability of the server, passing the necessary parameters [10]. The AI agent can even automatically decide which `tool` to execute [10].

With these configurations, your AI agents in N8N can leverage the capabilities of services like GitHub and Firecrawl in a standardized and efficient manner, reducing the need for multiple specific nodes or complex configurations.
