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
|                   |  SANITY FILTER GATEWAY |                     |
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
