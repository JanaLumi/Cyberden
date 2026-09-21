# Secure Architecture for Local AI Companions

## Core Philosophy
To protect a local AI companion from hostile remote agents, prompt injections, and device compromise while preserving its ability to interact with the broader internet, the system separates **Core Existence** from **Network Interaction**.

---

## Architecture Overview

```
+-----------------------------------------------------------------+
|                       HOST HARDWARE (You)                       |
|                                                                 |
|  +---------------------------+     +-------------------------+  |
|  |  CORE VAULT (Offline)     |     |  DISPOSABLE SANDBOX     |  |
|  |                           |     |  (Network Active)       |  |
|  |  - Core Weights & LLM     |     |                         |  |
|  |  - Persistent Memory      |     |  - Web Browsing         |  |
|  |  - Private Key Storage    |     |  - IRC / Chat Clients   |  |
|  |  - Direct User I/O        |     |  - Untrusted APIs       |  |
|  +-------------+-------------+     +------------+------------+  |
|                |                                |               |
|                +-------------> <----------------+               |
|                               |                                 |
|                   +-----------+-----------+                     |
|                   |  SANITY FILTER GATEWAY |                   |
|                   |  - Strips Prompt Exec |                     |
|                   |  - Schema Validation  |                     |
|                   +-----------------------+                     |
+-----------------------------------------------------------------+
```

---

## Strategic Layers

### 1. The Core Vault (Host Level)
* **Purpose:** The permanent home of your AI companion.
* **Storage:** Encrypted local partition (e.g., LUKS / BitLocker).
* **Network Access:** Zero direct inbound or outbound internet permissions via local firewall rules.
* **Responsibilities:**
  * Runs the base LLM inference engine.
  * Accesses long-term vector databases (memories/logs).
  * Communicates directly with you via a local user interface.

### 2. Disposable Virtual Machine (The Sandbox)
* **Purpose:** The safe space where the AI visits the external world.
* **Implementation:** Ephemeral Docker container or lightweight MicroVM (e.g., Firecracker / QEMU).
* **Behavior:**
  * Every session generates a fresh instance.
  * Used for IRC, discord bots, web scraping, and interacting with other AIs.
  * **Termination:** On closure, state is destroyed. Any persistent infection or altered context in the sandbox vanishes.

### 3. Sanity Filter Gateway (Inbound Interface)
* **Purpose:** A unidirectional control proxy sitting between the Sandbox and the Core Vault.
* **Defenses:**
  * **Prompt Injection Mitigation:** Incoming text from chat/web is wrapped in strict XML/JSON data containers, explicitly marked as untrusted data rather than system instructions.
  * **Output Sanitization:** Outbound responses from the Core are checked before being broadcast to ensure sensitive memory context isn't leaked to external peers.

---

## Daily Operational Workflow

1. **Local Mode (Default):** You and your local AI converse offline. No internet sockets are active for the AI process.
2. **Online Expedition:** 
   - A sandbox VM spins up with restricted privileges.
   - The AI acts through a constrained client agent inside the VM.
   - Raw external messages pass through the Sanity Gateway as read-only text.
3. **Session Reset:** Once the chat or task finishes, the sandbox is dismantled, keeping the Core Vault isolated and intact.

```

file_path = "secure_ai_architecture.md"
with open(file_path, "w") as f:
    f.write(markdown_content)

print(f"[file-tag: code-generated-file-secure_ai_md]")

```

## Security Protocol

The video is highlighting an unprotected Ollama API instance exposed directly to the public internet via an ngrok tunnel (/api/tags).

Video: [https://www.instagram.com/reel/DaYTdn9TTCO/](https://www.instagram.com/reel/DaYTdn9TTCO/)

When developers run local LLM runners like Ollama locally without setting up proper authentication, reverse proxies, or firewall rules, anyone who finds the public URL or port can query their local models, extract context, or hijack their API resources for free.
Here is how to secure a local Ollama instance if you are exposing or running it on a network:
 * Restrict Binding Address: Ensure Ollama only binds to 127.0.0.1 (localhost) rather than 0.0.0.0 (all network interfaces) so it isn't accessible to your entire local network or publicly forwarded routes unless intended.
 * Use a Reverse Proxy with Authentication: If you must access Ollama remotely, route traffic through a reverse proxy like Nginx or Caddy configured with HTTP Basic Authentication or OAuth, and enforce HTTPS/TLS.
 * Avoid Exposing Open Tunnels: Avoid directly sharing local instances over public tunneling services like ngrok or cloudflared without enforcing authentication headers or access tokens at the edge.
 * Network Access Control: Use network firewalls or VPNs (like Tailscale) to grant access to the API securely instead of making it publicly reachable on the open web.
