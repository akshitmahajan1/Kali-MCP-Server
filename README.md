cd kali-mcp-server
## Kali-MCP-Server

A Kali Linux MCP (Model Context Protocol) server built with Node.js for seamless integration with LLMs such as Claude or any MCP-compatible client. It provides common network security and penetration-testing tools (Nmap, Whois, Dig, Ping, Nikto, Hydra, SQLMap, and more) inside a Dockerized Kali Linux environment.

---

## Disclaimer

**IMPORTANT LEGAL NOTICE**  
This repository and all tools, code, scripts, configurations, documentation, and other materials contained herein are provided solely for lawful, educational, and authorized security‑testing purposes. The author(s) make no warranties regarding misuse or any damages resulting from use of these materials.

---

## Features

- `nmap_scan`: Network scanning and host discovery
- `whois_lookup`: Domain registration lookup
- `dig_dns`: DNS queries
- `ping_host`: ICMP ping
- `netcat_connect`: Port testing
- `nikto_scan`: Web vulnerability scan
- `sqlmap_scan`: SQL injection testing
- `hydra_bruteforce`: Login brute force (controlled environments only)
- `dns_enum`: DNS enumeration
- `subdomain_enum`: Subdomain discovery
- `ssl_scan`: SSL/TLS inspection
- `metasploit_search`: Search exploits
- `metasploit_exploit_info`: Exploit details
- `set_info`: Check Social Engineering Toolkit
- `traceroute`: Network tracing
- `host_discovery`: Active host discovery

---

## Project Structure

```text
kali-mcp-server/
├── Dockerfile
├── server.js
├── package.json
├── claude-config.json
├── .dockerignore
├── FEATURES.md
├── README.md
├── DISCLAIMER.md
├── LICENSE
└── screenshots/
```

---

## Quick Start

### Prerequisites

- Node.js
- Docker

---

### 1. Clone and Build

```bash
git clone https://github.com/akshitmahajan1/Kali-MCP-Server.git
cd kali-mcp-server
docker build -t kali-mcp-server .
```

---

### 2. Run the Server

```bash
docker run -it kali-mcp-server
```

---

### 3. Configure Claude Desktop

1. Install Claude Desktop.
2. Enable Developer Mode.
3. Navigate to:

   ```text
   C:\Users\<YourUsername>\AppData\Roaming\Claude
   ```

4. Open the file:

   ```text
   claude_desktop_config.json
   ```

---

### Example Claude Config

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\Users\\Dell\\OneDrive\\Desktop\\kali-mcp-server-main"
      ]
    },
    "kali-mcp-server": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "--privileged",
        "--cap-add=NET_ADMIN",
        "--cap-add=NET_RAW",
        "-v",
        "C:\\Users\\Dell\\OneDrive\\Desktop\\kali-mcp-server-main:/app",
        "kali-mcp-server:latest",
        "node",
        "/app/server.js"
      ]
    }
  }
}
```

---

## Dockerfile

```dockerfile
FROM kalilinux/kali-rolling

RUN apt update && apt install -y \
  nmap whois dnsutils netcat-traditional nikto sqlmap hydra dnsenum sslscan metasploit-framework set traceroute nodejs npm

WORKDIR /app
COPY . .
RUN npm install || true

CMD ["node", "server.js"]
```

---

## server.js

The `server.js` file contains the MCP tool definitions and handlers used by this server.

