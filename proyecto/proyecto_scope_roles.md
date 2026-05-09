---
fecha: 2026-05-02
tipo: Avance
proyecto: HookSuite
---

# HookSuite — Scope completo de todos los roles

## Contexto
Registro de todos los entregables concretos de cada rol. Es la referencia para hacer seguimiento del avance de cada miembro del equipo.

## Contenido

---

## P1 — Frontend (26 entregables en 8 bloques)

**Bloque 01 — Estructura base**
1. Proyecto React con Vite inicializado
2. Sistema de diseño base (Button, Badge, Spinner, Panel)
3. Layout principal con React Router y sidebar
4. Mocks de datos para desarrollo independiente

**Bloque 02 — Módulo Proxy / Interceptor**
5. Hook de WebSocket conectado al backend de P2
6. Panel de peticiones interceptadas con filtros
7. Vista detalle de petición con tabs
8. Onboarding guiado del PAC con verificación en tiempo real
9. Importador de peticiones raw HTTP y cURL

**Bloque 03 — Módulo Repeater**
10. Editor de petición HTTP con headers editables
11. Panel de respuesta (Raw, Pretty, Preview)
12. Comparador de respuestas (diff visual)
13. Historial de peticiones enviadas

**Bloque 04 — Módulo Intruder**
14. Configuración de ataque con punto de inyección visual
15. Panel de progreso del ataque en tiempo real
16. Tabla de resultados con flag de IA

**Bloque 05 — Panel de vulnerabilidades y red**
17. Dashboard de alertas por severidad
18. Detalle de vulnerabilidad con evidencias
19. Panel de red en tiempo real con paquetes marcados

**Bloque 06 — Utilidades**
20. Encoder / Decoder (Base64, URL, HTML, JWT)
21. Hash Generator (MD5, SHA1, SHA256, SHA512)
22. Regex Tester con resaltado de matches
23. Payload Generator visual

**Bloque 07 — Integración y UX final**
24. Conexión con backend real de P2
25. Estados de carga, errores y estados vacíos

**Bloque 08 — Documentación**
26. Capturas para informe PDF, manual de uso y script de demo

---

## P2 — Backend (28 entregables en 8 bloques)

**Bloque 01 — Servidor base**
1. FastAPI configurado con CORS
2. WebSocket server con gestión de sesiones multiusuario
3. Endpoint /health y /check/alive
4. Gestión de sesiones por token UUID

**Bloque 02 — Proxy HTTP interceptor**
5. Modelos Pydantic para todas las entidades
6. Servicio de proxy HTTP con httpx asíncrono
7. Archivo PAC generado dinámicamente
8. Endpoint de verificación del proxy
9. Proxy TCP real con mitmproxy en puerto 8080
10. Emisión de eventos interceptados al WebSocket de P1

**Bloque 03 — Repeater**
11. Endpoint de reenvío manual POST /api/repeater/send
12. Parser de raw HTTP
13. Parser de cURL
14. Historial de peticiones por sesión

**Bloque 04 — Intruder**
15. Biblioteca de payloads (SQLi, Blind SQLi, XSS, fuzzing)
16. Motor de fuzzing asíncrono con asyncio.Semaphore
17. Control de paralelismo y velocidad
18. Endpoints start/pause/cancel del ataque

**Bloque 05 — Utilidades**
19. Hash Generator API
20. Encoder/Decoder API
21. Regex Tester API

**Bloque 06 — Receptor de red**
22. Endpoint receptor de paquetes de P4

**Bloque 07 — Despliegue**
23. Dockerfile del backend
24. Docker Compose del proyecto completo
25. Nginx como proxy inverso con soporte WebSocket
26. VPS Hetzner CX22 aprovisionado con HTTPS

**Bloque 08 — Documentación**
27. Diagrama de arquitectura técnica
28. Guía de despliegue paso a paso

---

## P3 — Playwright (20 entregables en 5 bloques)

**Bloque 01 — Setup**
1. Playwright MCP instalado y optimizado (page.fill vs page.type)
2. DVWA en Docker como entorno de pruebas
3. Benchmark de velocidad documentado
4. Paralelismo con asyncio.Semaphore configurado

**Bloque 02 — Reconocimiento**
5. Sistema de autenticación (login en DVWA y genérico)
6. Spider/crawler con algoritmo BFS
7. Form Discoverer con soporte AJAX
8. Tech Fingerprinter (9 tecnologías)

**Bloque 03 — Automatización de ataques**
9. Rellenado automático de formularios con payloads
10. Captura de screenshots antes y después de ataques
11. Detección de anomalías en respuestas
12. Blind SQLi boolean-based automatizado
13. Blind SQLi time-based automatizado
14. Event Reporter para envío de resultados a P2

**Bloque 04 — Orquestación con IA**
15. Receptor de instrucciones de P5
16. Flujo de ataque completo dirigido por IA
17. Reporte de acciones en tiempo real al backend

**Bloque 05 — Demo y documentación**
18. Script de demo preparado y ensayado
19. Grabación de backup de la demo
20. Evidencias de vulnerabilidades encontradas en DVWA

---

## P4 — Chrome DevTools (22 entregables en 6 bloques)

**Bloque 01 — Setup CDP**
1. Chrome Launcher con --remote-debugging-port=9222
2. Verificación de acceso a los 4 dominios CDP (Network, Console, DOM, Runtime)
3. CDP Client WebSocket funcional
4. Packet Builder con formato JSON acordado validado con P2 y P5

**Bloque 02 — Captura de red**
5. Interceptor de peticiones HTTP/HTTPS
6. Captura de respuestas del servidor
7. Captura del body de respuesta
8. Captura del payload de peticiones POST
9. Filtrado de tráfico irrelevante (CDNs, imágenes, fuentes)
10. Pipeline de entrega de paquetes al backend de P2

**Bloque 03 — Captura de consola**
11. Interceptor de logs de consola
12. Detección de 11 patrones sensibles (API keys, passwords, paths, SQL errors)
13. Captura de errores de red

**Bloque 04 — Análisis de tráfico**
14. Detección de 5 headers de seguridad ausentes
15. Detección de cookies de sesión sin flags de seguridad
16. Correlación petición-respuesta con métricas de comportamiento
17. Marcado de tráfico sospechoso en tiempo real

**Bloque 05 — Road Map**
18. Road map de Práctica 2 con 10 mejoras y estimaciones concretas

**Bloque 06 — Documentación**
19. Capturas para informe PDF
20. Documentación técnica del módulo

---

## P5 — IA + GitHub (22 entregables en 5 bloques)

**Bloque 01 — GitHub**
1. Repositorio estructurado con 5 ramas de módulo
2. CONTRIBUTING.md con convención de commits
3. Protección de rama main
4. Pipeline GitHub Actions de despliegue automático
5. Revisión semanal del repositorio cada viernes

**Bloque 02 — IA: análisis**
6. Cliente Anthropic con reintentos exponenciales
7. Prompt de análisis de paquetes de red (JSON estructurado)
8. Prompt de análisis de resultados del Intruder
9. Prompt de análisis de errores de consola
10. Prompt de análisis de fingerprint y priorización de ataques
11. Clasificador de vulnerabilidades con umbral de confianza 60%

**Bloque 03 — IA: orquestación**
12. Orquestador del ciclo completo de ataque
13. Generación de instrucciones para P3
14. Sistema de confirmación de vulnerabilidades (2 confirmaciones)
15. Clasificación OWASP y generación de ficha completa

**Bloque 04 — Informe PDF**
16. Plantilla Typst profesional
17. Redacción de secciones transversales (portada, resumen, conclusiones)
18. Integración de secciones de cada rol
19. Verificación de los 10 puntos del enunciado
20. Generación del PDF final

**Bloque 05 — Entrega**
21. Revisión y merge de Pull Requests de todos los roles
22. Estado final del repositorio verificado y limpio

## Impacto
Este documento permite hacer seguimiento semanal del avance de cada rol y detectar retrasos antes de que impacten en la entrega.
