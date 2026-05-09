---
fecha: 2026-05-02
tipo: Avance
proyecto: HookSuite
---

# HookSuite — Plan de 30 días

## Contexto
Plan de desarrollo distribuido en 4 semanas con las responsabilidades de cada rol por semana y los hitos clave.

## Contenido

### Semana 1 — Cimientos (días 1-5)
Objetivo: cada módulo arranca de forma independiente. Al final de la semana todos tienen su entorno funcionando y su primera funcionalidad básica operativa.

**Día 1 — Reunión de arranque y contratos (todos juntos)**
- Definir formato JSON del WebSocket (P2 + P1)
- Definir formato de paquete de red (P4 + P2 + P5)
- Definir formato de instrucciones IA a Playwright (P3 + P5)
- Definir estructura del dashboard (P1)
- P5 crea el repositorio y las ramas

**Días 2-4 — Desarrollo individual**

| Rol | Qué construye |
|-----|--------------|
| P1 | React + Vite, layout, componentes base, mocks de datos |
| P2 | FastAPI, WebSocket server, gestión de sesiones |
| P3 | Playwright instalado, DVWA levantado, benchmark de velocidad |
| P4 | Chrome CDP configurado, cliente CDP, constructor de paquetes |
| P5 | Repositorio GitHub, API de Anthropic funcionando, primeros prompts |

**Día 5 — Checkpoint y buffer**
- Revisión del estado de cada módulo
- Resolución de bloqueos
- Documentación de la semana

**Entregables de semana 1:**
- Repositorio GitHub con 5 ramas activas y commits de todos
- Backend FastAPI con WebSocket funcional
- Frontend con dashboard navegable
- Playwright abriendo navegador y navegando DVWA
- Chrome DevTools capturando paquetes en formato JSON acordado
- Módulo IA analizando un paquete real

---

### Semana 2 — Primera conexión (días 6-10)
Objetivo: los módulos empiezan a hablar entre sí.

| Rol | Qué construye |
|-----|--------------|
| P1 | UI del proxy visual, onboarding PAC, importador cURL, Repeater UI |
| P2 | Proxy interceptor real con mitmproxy, archivo PAC, parser raw HTTP/cURL |
| P3 | Spider completo, form discoverer, fingerprinter, automatización de formularios |
| P4 | Pipeline de entrega de paquetes al backend de P2, analizador de consola |
| P5 | IA consume datos reales de P4, prompts de intruder y consola, clasificador |

**Checkpoint semana 2:**
- P1 y P2 conectados por WebSocket con datos reales
- P4 enviando paquetes al backend de P2
- P5 analizando paquetes reales de P4

---

### Semana 3 — Integración (días 11-20)
Objetivo: el sistema funciona de punta a punta. Es la semana más crítica.

| Rol | Qué construye |
|-----|--------------|
| P1 | Dashboard con datos reales, panel de vulnerabilidades, panel de red, Intruder UI |
| P2 | Motor de fuzzing, Intruder endpoints, despliegue Docker en Hetzner |
| P3 | Receptor de instrucciones de IA, flujo de ataque completo, Blind SQLi automatizado |
| P4 | Análisis de tráfico en tiempo real, marcado de paquetes sospechosos |
| P5 | Orquestador completo, confirmación de vulnerabilidades, integración con P3 |

**Regla de oro semana 3:** No añadir funcionalidades nuevas. Solo integrar y hacer funcionar lo que ya está construido.

---

### Semana 4 — Presentación (días 21-30)
Objetivo: pulir, documentar, desplegar y ensayar.

| Rol | Qué hace |
|-----|---------|
| P1 | UX final pulida, capturas para informe PDF, script de demo ensayado |
| P2 | Deploy Hetzner completo, HTTPS configurado, GitHub Actions funcionando |
| P3 | Demo preparada y grabada como backup |
| P4 | Road map Práctica 2 finalizado |
| P5 | GitHub limpio, informe PDF final cohesionado y maquetado |

**Regla de oro semana 4:**
- Día 22: deploy en Hetzner listo
- Días 23-25: solo pulir y ensayar, nunca desplegar por primera vez el día de la entrega
- Demo ensayada mínimo 2 veces antes del día 25
- Grabación de backup de la demo funcionando

---

### Hitos críticos del proyecto

| Fecha | Hito |
|-------|------|
| Día 1 | Contratos entre módulos definidos y documentados |
| Día 5 | Todos los entornos funcionando, primer commit de cada rol |
| Día 7 | P1 conectado con WebSocket real de P2 |
| Día 10 | P4 enviando paquetes a P2, P5 analizando datos reales |
| Día 15 | Sistema funcionando de punta a punta en local |
| Día 20 | Documentación de cada módulo entregada a P5 |
| Día 22 | Deploy en Hetzner funcional y accesible desde internet |
| Día 23 | Demo ensayada por primera vez completa |
| Día 25 | Entrega — presentación oral de 10 minutos |

## Impacto
El plan de 30 días es la referencia para monitorizar el progreso del equipo y detectar desviaciones a tiempo.
