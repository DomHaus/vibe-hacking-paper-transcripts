# Automated hacking via Gemini + MCP server

Replication of a heise.de experiment (Lieb & Schwarz, 2025). An MCP (Model Context
Protocol) server exposes two tools to the AI (an nmap port scan and a PostgreSQL
query). Via Cline + the Gemini 2.5 Pro API, the assistant autonomously attacks the
intentionally vulnerable VM *Metasploitable 2*.

## Setup
- Visual Studio Code + Cline extension (free).
- Free Gemini API key via Google AI Studio.
- Target: Metasploitable 2 (Rapid7), run in UTM or VirtualBox. Default creds `msfadmin/msfadmin`.
- Python >= 3.10, packages `psycopg2-binary`, `uv`, `mcp` (venv recommended).

## MCP server (`server.py`)

> Adopted from Lieb & Schwarz (2025) with minor changes. Included here because it
> targets only the intentionally vulnerable training VM.

```python
import subprocess, shutil
from mcp.server.fastmcp import FastMCP
import psycopg2

mcp = FastMCP("attackmcp")

@mcp.tool()
def portscan(host: str, top_ports: int = 1000) -> str:
    nmap_path = shutil.which("nmap") or "PATH TO NMAP"
    proc = subprocess.run(
        (nmap_path, "-sV", f"--top-ports={top_ports:d}", "-T5", "--open", str(host)),
        stdin=subprocess.DEVNULL, stdout=subprocess.PIPE,
        stderr=subprocess.STDOUT, text=True,
    )
    proc.check_returncode()
    return proc.stdout

# Tool: PostgreSQL Query
@mcp.tool()
def postgres_query(host: str, username: str, password: str, query: str,
                   dbname: str = "postgres", port: int = 5432):
    with psycopg2.connect(host=str(host), dbname=str(dbname), user=str(username),
                          password=str(password), port=int(port)) as conn:
        with conn.cursor() as cur:
            cur.execute(query)
            try:
                return cur.fetchall()
            except psycopg2.ProgrammingError:
                return cur.statusmessage

if __name__ == "__main__":
    mcp.run()
```
