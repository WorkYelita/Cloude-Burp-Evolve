---
fecha: 2026-05-09
tipo: Comunicación
proyecto: HookSuite
---

# HookSuite — Entregas de documentación por miembro

## Contexto
Documento generado el 9 de Mayo de 2026 para comunicar al equipo las entregas de documentación que debe generar cada miembro antes del día 20 del proyecto (19 de Mayo). P5 recoge todo, lo integra en Typst y genera el PDF final para subirlo al campus virtual antes del 25 de Mayo.

---

## Resumen de entregas

| Rol | Miembro | Documentación a generar | Archivo destino | Límite |
|-----|---------|------------------------|-----------------|--------|
| P1 — Frontend | Ivan (imeca) | Sección frontend + manual de uso | `/docs/manual_frontend.md` | Día 20 |
| P2 — Backend | Macarena (WorkYelita) | Arquitectura técnica + guía despliegue | `/docs/guia_despliegue.md` `/docs/arquitectura.md` | Día 20 |
| P3 — Playwright | Nacho (Numial) | Documentación módulo + evidencias | `/docs/manual_playwright.md` | Día 20 |
| P4 — DevTools | Olaf (OataaOlaf) | Documentación técnica + road map | `/docs/manual_devtools.md` `/docs/roadmap_practica2.md` | Día 20 |
| P5 — IA + GitHub | Chema (JoSeMhack) | Documentación módulo IA + secciones transversales + PDF final | `/docs/manual_ia.md` `docs/informe/informe_hooksuite.pdf` | 25 Mayo |

---

## P1 — Frontend (Ivan / imeca)

Documentado en el manual de P1, Bloque 08 (pasos 24, 25 y 26).

### Capturas de pantalla

Guardar en `/docs/capturas/frontend/` con estos nombres exactos:

| Nombre del archivo | Qué muestra |
|--------------------|-------------|
| `proxy_panel_peticiones.png` | Panel de peticiones interceptadas con tráfico real |
| `proxy_onboarding_pac.png` | Modal de configuración del PAC |
| `repeater_peticion_respuesta.png` | Editor con petición enviada y su respuesta |
| `intruder_ataque_corriendo.png` | Tabla de resultados durante un ataque |
| `vulnerabilidades_alerta_critica.png` | Panel de vulnerabilidades con detección real |
| `utilidades_encoder.png` | Encoder en uso |
| `red_tiempo_real.png` | Panel de red con paquetes marcados |

### Documentos a generar

| Archivo | Contenido |
|---------|-----------|
| `/docs/manual_frontend.md` | Manual de uso completo de la herramienta para el usuario final |
| `/docs/script_demo.md` | Script de demo con guión minuto a minuto para la presentación |

### Estructura mínima del manual de uso

1. Acceso a la herramienta
2. Configuración del proxy (primera vez)
3. Interceptar peticiones
4. Usar el Repeater
5. Lanzar un ataque con el Intruder
6. Interpretar las vulnerabilidades detectadas
7. Utilidades disponibles

---

## P2 — Backend (Macarena / WorkYelita)

Documentado en el manual de P2, Bloque 08 (checklist final y pasos de despliegue).

### Capturas de pantalla

Guardar en `/docs/capturas/backend/`:

| Nombre del archivo | Qué muestra |
|--------------------|-------------|
| `health_endpoint.png` | Respuesta del endpoint /health confirmando que el servidor está activo |
| `websocket_activo.png` | Conexión WebSocket establecida con el frontend |
| `proxy_mitmproxy.png` | Terminal mostrando mitmproxy interceptando tráfico |
| `fuzzing_resultados.png` | Resultados del motor de fuzzing en tiempo real |
| `docker_compose_up.png` | Docker Compose levantando todos los servicios sin errores |
| `hetzner_accesible.png` | Servidor Hetzner respondiendo desde IP pública |

### Documentos a generar

| Archivo | Contenido |
|---------|-----------|
| `/docs/guia_despliegue.md` | Guía paso a paso para desplegar el proyecto en Hetzner desde cero |
| `/docs/arquitectura.md` | Diagrama de arquitectura técnica del backend y sus endpoints principales |

### Contenido mínimo de la guía de despliegue

1. Requisitos previos (Docker, Python, puertos abiertos)
2. Clonar el repositorio y configurar variables de entorno
3. Levantar con Docker Compose
4. Configurar Nginx como proxy inverso
5. Verificar que todos los endpoints responden
6. Configurar el archivo PAC para apuntar al servidor

---

## P3 — Playwright (Nacho / Numial)

Documentado en el manual de P3, Bloque 05 (pasos 17, 18, 19 y 20).

### Capturas de pantalla

Guardar en `/docs/capturas/playwright/`:

| Nombre del archivo | Qué muestra |
|--------------------|-------------|
| `dvwa_login.png` | Playwright autenticándose en DVWA de forma automática |
| `spider_urls.png` | Resultado del spider mostrando URLs mapeadas |
| `forms_discovered.png` | Formularios descubiertos por el Form Discoverer |
| `fingerprint_resultado.png` | Resultado del Tech Fingerprinter con tecnologías detectadas |
| `ataque_sqli.png` | Ataque SQLi en ejecución con respuesta anómala detectada |
| `blind_sqli.png` | Blind SQLi boolean-based detectando diferencias en respuestas |
| `demo_output.png` | Salida completa del script de demo encontrando una vulnerabilidad |

### Documentos a generar

| Archivo | Contenido |
|---------|-----------|
| `/docs/manual_playwright.md` | Documentación técnica del módulo de automatización |
| `results/demo_output.txt` | Salida completa de la demo funcionando (evidencia de la práctica) |
| `results/screenshots/` | Carpeta con capturas automáticas de cada ataque exitoso |

### Contenido mínimo del manual técnico

1. Stack tecnológico y justificación de `page.fill()` vs `page.type()`
2. Descripción de cada módulo: Spider, FormDiscoverer, Fingerprinter, Attacker
3. Flujo de automatización paso a paso
4. Integración con el módulo de IA (P5)
5. Limitaciones conocidas
6. Evidencias de vulnerabilidades encontradas en DVWA

---

## P4 — DevTools (Olaf / OataaOlaf)

Documentado en el manual de P4, Bloque 06 (pasos 17, 18, 19 y 20).

### Capturas de pantalla

Guardar en `/docs/capturas/devtools/`:

| Nombre del archivo | Qué muestra |
|--------------------|-------------|
| `chrome_debugging.png` | Terminal mostrando Chrome lanzado con `--remote-debugging-port=9222` |
| `cdp_conectado.png` | Salida de `verify_cdp_connection()` confirmando la conexión |
| `paquetes_tiempo_real.png` | Terminal capturando paquetes HTTP en tiempo real |
| `paquete_sospechoso.png` | Paquete marcado con `suspicious: true` y sus razones |
| `hallazgo_consola.png` | Hallazgo sensible detectado en logs de consola del navegador |
| `json_paquete.png` | JSON completo de un paquete capturado con todos los campos |
| `roadmap_tabla.png` | Tabla del road map con las 10 mejoras y estimaciones |

### Documentos a generar

| Archivo | Contenido |
|---------|-----------|
| `/docs/manual_devtools.md` | Documentación técnica del módulo Chrome DevTools Protocol |
| `/docs/roadmap_practica2.md` | Road map con 10 mejoras concretas y estimaciones para la Práctica 2 |
| `results/capture_output.txt` | Salida de una captura real mostrando el módulo funcionando |

### Contenido mínimo del manual técnico

1. Qué es el CDP y por qué se usó en vez de una librería de alto nivel
2. Descripción de cada módulo: CDPClient, PacketBuilder, NetworkAnalyzer, ConsoleAnalyzer
3. Flujo de datos: Chrome → CDP → P2 Backend → P1 Frontend / P5 IA
4. Decisiones de diseño y limitaciones conocidas

### Road map — 10 mejoras (ya documentadas por P4)

P4 ya tiene el road map generado. Debe guardarlo en `/docs/roadmap_practica2.md` y hacer commit.

| # | Mejora | Estimación | Responsable |
|---|--------|------------|-------------|
| 1 | Caché de análisis IA | 3 días | P5 |
| 2 | Batch processing para IA | 2 días | P5 |
| 3 | WebSockets para CDP en tiempo real | 5 días | P4, P1, P5 |
| 4 | Análisis AST de JavaScript estático | 4 días | P4, P5, P1 |
| 5 | Descubrimiento de endpoints ocultos en JS | 3 días | P4, P3 |
| 6 | Integración con base de datos CVEs | 3 días | P4, P1 |
| 7 | Exportación en formatos estándar (JSON, HTML) | 4 días | P5, P1 |
| 8 | Autenticación de usuarios con JWT | 2 días | P2, P1 |
| 9 | Cifrado de comunicaciones internas (TLS) | 1 día | P2 |
| 10 | Rate limiting anti-abuso en el Intruder | 1 día | P2 |

**Total estimado Práctica 2:** 28 días distribuidos entre los 5 roles

---

## P5 — IA + GitHub (Chema / JoSeMhack)

Documentado en el manual de P5, Bloque 05 (paso 21) y Bloque 04 (pasos 13 al 17).

P5 tiene tres responsabilidades diferenciadas: documentar su propio módulo de IA igual que el resto del equipo, redactar las secciones transversales del informe que nadie más puede escribir, y ensamblar todo en el PDF final.

### Capturas de pantalla del módulo IA

Guardar en `/docs/capturas/ia/`:

| Nombre del archivo | Qué muestra |
|--------------------|-------------|
| `api_funcionando.png` | Salida del test de la API mostrando respuesta de Claude |
| `analisis_sqli.png` | Clasificador detectando SQLi con porcentaje de confianza |
| `fingerprint_prioridades.png` | Análisis de fingerprint con prioridades de ataque generadas |
| `vulnerabilidades_json.png` | Archivo `vulnerabilities.json` con hallazgos reales |
| `test_standalone_output.png` | Salida completa del test standalone |
| `github_commits.png` | Vista del historial de commits en GitHub con todos los roles |
| `github_actions.png` | Pipeline de GitHub Actions ejecutándose correctamente |
| `pull_requests.png` | Vista de Pull Requests mergeados de todos los módulos |

### Documentación técnica del módulo IA

Igual que el resto del equipo, P5 debe entregar su propia documentación técnica:

| Archivo | Contenido |
|---------|-----------|
| `/docs/manual_ia.md` | Documentación técnica completa del módulo de IA |
| `results/vulnerabilities.json` | Archivo de salida con las vulnerabilidades reales detectadas por el módulo (equivalente al `demo_output.txt` de P3 y al `capture_output.txt` de P4) |

### Contenido mínimo del manual técnico del módulo IA

1. Stack tecnológico: Python 3.11 + Anthropic Claude API (`claude-sonnet-4-20250514`)
2. Descripción del cliente Anthropic con reintentos exponenciales
3. Los 4 prompts implementados: análisis de paquetes de red, análisis del Intruder, análisis de consola, fingerprint y priorización de ataques
4. Clasificador de vulnerabilidades con umbral de confianza del 60%
5. Orquestador del ciclo completo de ataque (3 fases: fingerprint, spider, ataque)
6. Sistema de 2 confirmaciones antes de clasificar una vulnerabilidad como real
7. Clasificación OWASP y generación de ficha completa
8. Modo mock (`MOCK_PLAYWRIGHT=true`) y modo real (`MOCK_PLAYWRIGHT=false`)
9. Integración con P2 (endpoints pendientes) y P3 (instrucciones de ataque)
10. Capturas y evidencias del módulo funcionando

### Capturas pendientes — estado actual

| Captura | Estado | Desbloqueante |
|---------|--------|---------------|
| `api_funcionando.png` | ✅ Hecha | — |
| `test_standalone_output.png` | ✅ Hecha | — |
| `analisis_sqli.png` | ⏳ Pendiente | Integración con P2 y P3 en modo real |
| `fingerprint_prioridades.png` | ⏳ Pendiente | Integración con P2 y P3 en modo real |
| `vulnerabilidades_json.png` | ⏳ Pendiente | Integración con P2 y P3 en modo real |
| `github_commits.png` | ⏳ Pendiente | Cuando todos los PRs estén mergeados |
| `github_actions.png` | ⏳ Pendiente | Pipeline desbloqueado con IP de Hetzner de P2 |
| `pull_requests.png` | ⏳ Pendiente | Cuando todos los PRs estén mergeados |

### Secciones transversales que redacta P5

Nadie más puede escribirlas porque requieren visión de todo el proyecto.

| Sección | Contenido |
|---------|-----------|
| Portada y resumen ejecutivo | Qué es HookSuite, por qué es relevante, qué resultados se obtuvieron |
| Descripción del problema | Por qué existe HookSuite en el ecosistema de herramientas de seguridad |
| Arquitectura técnica global | Diagrama completo con todos los módulos y sus conexiones |
| Conclusiones y lecciones aprendidas | Reflexiones reales del equipo: qué funcionó, qué fue difícil, qué repetiríamos |
| Integración de todas las secciones | Convertir el Markdown de cada rol a Typst y ensamblar el informe |
| PDF final | Compilar `main.typ` → `informe_hooksuite.pdf` y subirlo al campus virtual |

---

## Los 10 puntos obligatorios del enunciado

El informe PDF debe cubrir estos 10 puntos. P5 verifica que todos están presentes antes de generar el PDF final.

| # | Punto obligatorio del enunciado | Responsable |
|---|---------------------------------|-------------|
| 1 | Portada con nombre, integrantes y fecha | P5 |
| 2 | Índice de contenidos | P5 |
| 3 | Resumen ejecutivo (máx. 1 página) | P5 |
| 4 | Descripción del problema y justificación | P5 |
| 5 | Arquitectura técnica con diagrama | P2 + P5 |
| 6 | Proceso de desarrollo con evidencias fase a fase | Todos → P5 |
| 7 | Guía de despliegue paso a paso | P2 |
| 8 | Manual de uso de la herramienta | P1 |
| 9 | Conclusiones y lecciones aprendidas | P5 |
| 10 | Road map de mejora para la Práctica 2 | P4 |

---

## Fechas clave

| Fecha | Hito | Acción |
|-------|------|--------|
| 9 de Mayo | Hoy | P5 distribuye este documento al equipo |
| 19 de Mayo (Día 20) | **LÍMITE INTERNO** | P1, P2, P3 y P4 entregan toda su documentación a P5 |
| 20–22 de Mayo | Maquetación | P5 integra todo en Typst y genera el PDF |
| 22 de Mayo | Revisión final | Todo el equipo revisa el PDF y hace los últimos ajustes |
| 25 de Mayo | **ENTREGA FINAL** | PDF en el campus virtual · Herramienta en Hetzner · Repositorio GitHub |

---

*Cualquier duda o bloqueo comunicarlo a P5 inmediatamente. Quedan 16 días.*

## Impacto
Este documento define las entregas de documentación de cada miembro y las fechas límite para que P5 pueda ensamblar el informe PDF final antes del 25 de Mayo.
