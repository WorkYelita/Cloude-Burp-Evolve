---
fecha: 2026-05-02
tipo: Conocimiento
proyecto: HookSuite
---

# HookSuite — Conocimiento técnico e investigación

## Contexto
Registro de la investigación técnica realizada durante la fase de diseño del proyecto y del conocimiento clave que sustenta las decisiones arquitectónicas.

## Contenido

### Investigación 01 — Limitaciones del navegador para un proxy web
**Fuente:** Investigación interna del equipo (Carlos trabajador + Chema)  
**Hallazgo:** El modelo de seguridad del navegador impide tres cosas fundamentales para un proxy interceptor:
1. No se puede interceptar tráfico de otras pestañas/apps (Same-Origin Policy)
2. No se puede actuar como proxy TCP (los browsers no tienen acceso a sockets TCP arbitrarios)
3. No se pueden modificar headers como Host, Origin, Cookie en fetch/XHR

**Conclusión:** La función core de Burp Suite es imposible si todo se hace en el frontend. La solución pasa por mover la lógica al backend del servidor.

---

### Investigación 02 — Opciones para el proxy interceptor
**Fuente:** Investigación interna del equipo (Chema)  
**Opciones evaluadas:**

| Opción | Resultado |
|--------|-----------|
| Extensión de navegador | ❌ Descartada — se sale del concepto de web app |
| Certificado CA propio | ❌ Descartada — requiere instalar certificado en el cliente |
| WebSockets como base | ✅ Seleccionada — solución limpia, sin instalaciones, multiusuario nativo |
| Proxy SOCKS5 | ❌ Descartada — configuración manual compleja |
| Enfoque híbrido Electron | ❌ Descartada — requiere instalar app de escritorio |
| Archivo PAC | ✅ Seleccionado para interceptación real — mínima fricción posible |
| Service Workers | ❌ Descartados — solo interceptan tráfico del propio dominio |

---

### Investigación 03 — Referente encontrado: Caido
**Fuente:** Investigación exhaustiva del equipo  
**Hallazgo:** Durante la investigación se descubrió Caido, una herramienta de seguridad web moderna con arquitectura cliente-servidor muy similar a la planteada. Caido corre el servidor remotamente en un VPS y el usuario se conecta a través del navegador. También requiere configuración manual del proxy en el navegador.  
**Conclusión:** Valida que la arquitectura propuesta es viable y está siendo usada en producción por profesionales. Confirma que no existe ninguna forma técnica de evitar el paso de configuración del proxy sin instalar una extensión o app.

---

### Investigación 04 — Propuesta del profesor Carlos (stack técnico)
**Fuente:** Sesión con Carlos (profesor del módulo)  
**Propuesta:** Playwright MCP + Chrome DevTools MCP + proxy interceptor + módulo IA que analiza respuestas y orquesta ataques automáticamente.  
**Optimización clave indicada:** En Playwright usar `page.fill()` en vez de `page.type()` para pasar el texto completo al campo de una vez. Mejora de velocidad x60. Paralelizar las ejecuciones según los recursos del servidor.  
**Valoración:** Arquitectura ambiciosa y técnicamente potente. Viable en 30 días con un equipo de 5 personas disciplinado.

---

### Investigación 05 — Arquitectura de comunicación entre módulos
**Fuente:** Diseño interno del proyecto  
**Decisiones técnicas:**
- WebSocket como canal de comunicación en tiempo real entre backend y frontend
- Formato JSON acordado para paquetes de red: id, method, url, status, size, time, timestamp, request_headers, request_body, response_headers, response_body, suspicious, vulnerable
- Formato JSON acordado para instrucciones de IA a Playwright: type, url, selector, payload, verify, session_token
- Sesiones aisladas por token UUID para soporte multiusuario

---

### Investigación 06 — Herramientas de IA recomendadas por la práctica
**Fuente:** Enunciado de la práctica  
**Herramientas permitidas:** Claude Code, Cursor, GitHub Copilot, Windsurf, ChatGPT/GPT4o, Claude (Anthropic), Gemini, Playwright MCP, LangChain, CrewAI, entre otras.  
**Elección del equipo:** Claude Code como IDE principal + Claude API (claude-sonnet-4-20250514) como motor de análisis de vulnerabilidades.  
**Motivo:** Claude Code es la herramienta con la que trabaja el profesor y el equipo tiene experiencia. claude-sonnet-4-20250514 ofrece el mejor equilibrio entre capacidad y coste para el caso de uso.

---

### Investigación 07 — Estimación de costes API de Anthropic
**Fuente:** Estimación interna  
**Estimación por sesión de auditoría:**
- Análisis de paquetes de red: ~0.002$ por paquete
- Sesión típica de 30 minutos en DVWA: ~50 paquetes = ~0.10$
- Análisis de resultados del Intruder (30 payloads): ~0.01$
- Coste total estimado por sesión: ~0.15$
- Coste total estimado para desarrollo y pruebas: < 5$

## Impacto
Este conocimiento fundamenta las decisiones arquitectónicas del proyecto y puede usarse para justificarlas ante el profesor en la presentación oral.
