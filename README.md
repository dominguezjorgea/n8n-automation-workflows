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
