---
fecha: 2026-05-02
tipo: Conocimiento
proyecto: HookSuite
---

# HookSuite — Propuesta técnica del profesor Carlos

## Contexto
Resumen procesado de la sesión con Carlos (profesor del módulo) donde propuso la arquitectura técnica del proyecto. Fuente original: transcripción de audio de la sesión.

## Contenido

### Propuesta principal
Carlos propuso construir una herramienta de auditoría web automatizada con IA combinando:

**Playwright MCP** — permite acceso al navegador desde Claude Code. Automatiza clicks, texto y navegación. Permite que la IA haga los clicks en vez del humano.

**Chrome DevTools MCP** — proporciona acceso al dominio Network del navegador, a la consola y al inspector. Permite capturar todos los paquetes de red, leer el payload enviado, la respuesta y renderizar la preview en HTML.

**Proxy interceptor propio** — construido con Python, equivalente al interceptor/repeater de Burp Suite. Con acceso a la red ya se tienen los paquetes. El proxy puede hacer clicks para automatizar la auditoría.

**Módulo de IA** — analiza las respuestas capturadas, determina si hay vulnerabilidades y orquesta el siguiente ataque.

### Optimizaciones técnicas indicadas

**Playwright — optimización de velocidad:**
Usar `page.fill()` en vez de `page.type()`. Por defecto Playwright simula pulsación tecla a tecla (tarda ~10 segundos para textos largos). Con `page.fill()` se pasa el texto completo al buffer de una vez. Mejora de velocidad: x65 aproximadamente.

**Paralelización:**
Abrir múltiples páginas en paralelo según los recursos del servidor. No sobrepasar el límite para no colapsar el servidor.

**Browser Use como alternativa:**
Carlos mencionó Browser Use (Python) como alternativa a Playwright. Su recomendación es optimizar Playwright en vez de usar Browser Use.

### Sobre los modelos de IA locales (Ollama)
Carlos desaconsejó usar Ollama (modelos locales) porque los modelos disponibles localmente son más antiguos y menos potentes que los modelos online. Recomendó usar Claude (Anthropic) que siempre tiene los modelos más recientes.

### Sobre el proxy en el servidor
Carlos resolvió la duda sobre cómo implementar el proxy en un servidor remoto: es exactamente igual que en local (interfaz + puerto), simplemente en un servidor más potente. Descartó la preocupación inicial y confirmó que montar el proxy en Hetzner es perfectamente viable.

### Sobre Claude Code
Carlos indicó que trabaja principalmente con Claude Code en el cliente de terminal y ha dejado de usar Cursor. Lo considera la herramienta más potente disponible actualmente para desarrollo asistido por IA.

## Impacto
La propuesta de Carlos es la base arquitectónica del proyecto. Sus optimizaciones técnicas están implementadas directamente en los manuales de P3 (Playwright) y P2 (Backend).
