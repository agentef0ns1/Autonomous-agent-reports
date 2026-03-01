

# Vulnerability assessments : using autonomous agents connected to a different local LLM

[![Autonomous - Vulnerability Assesment ](https://img.youtube.com/vi/bEM2UU-0e5Q/0.jpg)](https://www.youtube.com/watch?v=bEM2UU-0e5Q)

## Definition

It is a set of 4 autonomous AI agents:
- All connect to a local LLM.

### Main function: 
```text
Vulnerability analysis and detection of known exploits for services exposed on a known target.
```
### The target:

will be the following docker deployed locally
```
vulhub/weblogic:10.3.6.0-2017 "startWebLogic.sh" .... cve-2017-10271-weblogic-1

https://github.com/vulhub/vulhub/blob/master/weblogic/CVE-2017-10271/README.md
```

### Architecture:

  - Orchestrator agent: connected to a neo4j database, where the state flow is defined, connected to a locally deployed LLM with ollama phi4-mini:latest, its function will be to manage the main process flow by invoking based on the state it is in and the decision it makes based on its possible paths, invoking each of the agents that will perform specialized functions.
  - Enumerator agent: its function is, given an asset, host, or network, to enumerate it with nmap, obtaining its open ports and the version of its services. Connected to a locally deployed LLM with ollama: etgohome/hackidle-nist-coder:v1.1, for decision-making.
  - Analyzer agent: based on the results obtained, it will collect the output from the enumerator agent and search for vulnerabilities for that service with searchsploit.
  - Report agent: responsible for obtaining data from previous processes and generating an executive report on the ports and possible vulnerabilities detected. Connected to a locally deployed LLM with ollama: etgohome/hackidle-nist-coder:v1.1, for decision-making.


# === REPORT AGENT SUMMARY ===

- **IP:** 127.0.0.1
- **Servicios/Versiones:**
  - 631/tcp - IPP - CUPS 2.4
  - 7001/tcp - HTTP - Oracle WebLogic Server 10.3.6.0 (Servlet 2.5; JSP 2.1; T3 enabled)
  - 8000/tcp - HTTP - Uvicorn

### Vulnerabilidades y Exploits Detectados:
- **CUPS:**
  - No se encontraron exploits específicos para CUPS 2.4.

- **Oracle WebLogic Server:**
  - Oracle WebLogic Server 10.3.6.0 es vulnerable a deserialización remota de comandos (Java Deserialization Remote Code Execution, Exploit Title).
  - Oracle Weblogic Server 10.3.6.0 / 12.1.3.0 / 12.2.1.2 / 12.2.1.3 es vulnerable a deserialización remota de comandos (Deserialization Remote Command Execution, Exploit Title).
  - Oracle Weblogic Server 10.3.6.0.0 / 12.x es vulnerable a deserialización remota de comandos (Remote Command Execution, Exploit Title).

- **Uvicorn:**
  - No se encontraron exploits específicos para Uvicorn.

### Recomendaciones:
- Actualizar Oracle WebLogic Server a la versión más reciente o aplicar parches de seguridad.
- Evitar exponer Oracle WebLogic Server en entornos no seguros, ya que es un componente comúnmente utilizado en aplicaciones empresariales.', thinking=None, images=None, tool_name=None, tool_calls=None) logprobs=None
