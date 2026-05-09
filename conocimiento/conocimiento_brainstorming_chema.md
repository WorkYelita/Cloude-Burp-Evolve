---
fecha: 2026-05-02
tipo: Conocimiento
proyecto: HookSuite
---

# HookSuite — Investigación técnica de Chema (P2)

## Contexto
Resumen procesado del documento de brainstorming técnico elaborado por Chema siguiendo el hilo de investigación de Carlos (trabajador). Fuente original: brainstorming_log.md de Abril 2026.

## Contenido

### Punto de partida
La pregunta que guió la investigación: ¿cómo gestionar el proxy en un servidor remoto multiusuario? Burp Suite funciona como proxy local, pero si la herramienta es una web app en un servidor compartido, hay que resolver el aislamiento de tráfico por usuario.

### Qué es factible en una web app

**Sí factible:**
- Request Builder/Editor
- Encoder/Decoder (Base64, URL, HTML, JWT)
- Hash Generator
- Comparador de respuestas (diff visual)
- Regex Tester
- Payload Generator
- Proxy visual como interfaz (con backend que haga el trabajo real)

**No factible directamente desde el navegador:**

| Limitación | Motivo |
|-----------|--------|
| No interceptar tráfico de otras pestañas | Same-Origin Policy |
| No actuar como proxy TCP | Los browsers no tienen acceso a sockets TCP |
| No modificar headers Host, Origin, Cookie | El browser los protege por diseño |

**Conclusión:** Si el proxy corre en el backend de Hetzner (Python o Node.js), el navegador es solo la interfaz visual. El servidor puede hacer TCP, modificar headers y actuar como proxy real.

### Opciones evaluadas para el proxy

**Opción 1 — Extensión de navegador**
Descartada. Se sale del concepto de web app pura.

**Opción 2 — Certificado CA propio**
Descartada. Requiere que el usuario instale un certificado en su máquina. Fricción considerable.

**Opción 3 — WebSockets ✅ SELECCIONADA**
El frontend conecta al backend mediante WebSocket. El usuario construye o pega una petición en la interfaz, el backend la ejecuta, intercepta la respuesta y la devuelve en tiempo real. Ventajas: sin instalaciones, multiusuario nativo con tokens de sesión. Limitación: no intercepta el tráfico real del navegador del usuario (las peticiones se construyen manualmente). Para el contexto de la práctica (SQLi, fuzzing) es suficiente.

**Opción 4 — Proxy SOCKS5**
Descartada. Requiere configuración manual compleja en el navegador.

**Opción 5 — Enfoque híbrido Electron**
Descartada. Requiere instalar una app de escritorio.

### Solución al problema del proxy real: archivo PAC ✅ SELECCIONADO

**Qué es:** Un fichero JavaScript alojado en el servidor que contiene la función `FindProxyForURL(url, host)`. El navegador lo lee antes de cada petición y decide si enrutar a través del proxy.

**Cómo se configura:** Una sola vez en la configuración del navegador (Chrome, Firefox, Edge, Safari). El usuario pega la URL del PAC y ya está. El servidor lo controla y puede actualizarlo sin que el usuario toque nada.

**Por qué es la mejor opción:** Compatible con todos los navegadores modernos. Mínima fricción posible sin instalar nada. Una vez configurado, el flujo es completamente transparente.

**Referente validador encontrado:** Caido — herramienta de seguridad web profesional con arquitectura cliente-servidor idéntica. También requiere configuración manual del proxy. Confirma que no existe ninguna forma técnica de evitar ese paso sin instalar algo.

### Solución a la UX del PAC: onboarding guiado ✅ SELECCIONADO

- Asistente que se lanza la primera vez
- Detecta el navegador y SO automáticamente
- Muestra instrucciones visuales paso a paso personalizadas
- Botón "Copiar URL del PAC" con feedback visual
- Verificación en tiempo real: el servidor comprueba si el proxy está activo cada 2 segundos
- Cuando está activo, el modal se cierra automáticamente

### Funcionalidad complementaria: importador de peticiones ✅ SELECCIONADO

El usuario copia una petición desde DevTools o Burp Suite (formato raw HTTP o cURL) y la pega en la app. La app detecta el formato automáticamente y rellena todos los campos del Repeater. Es más accesible a primera vista que el PAC pero más tedioso en sesiones largas de pentesting.

### Service Workers descartados
Solo interceptan tráfico del propio dominio. No sirven para auditar sitios de terceros.

## Impacto
Esta investigación es la base técnica que justifica las decisiones de arquitectura del proyecto. El documento de brainstorming original es evidencia del proceso de investigación para el informe PDF.
