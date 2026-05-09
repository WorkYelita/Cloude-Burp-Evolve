---
fecha: 2026-05-02
tipo: Avance
proyecto: HookSuite
---

# HookSuite — Arquitectura técnica

## Contexto
Descripción detallada de la arquitectura técnica del proyecto, los módulos que la componen y cómo se comunican entre sí.

## Contenido

### Diagrama de arquitectura

```
┌─────────────────────────────────────────────────────────────┐
│                    SERVIDOR HETZNER CX22                    │
│                  Docker + Nginx + GitHub CI/CD              │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              P1 — FRONTEND (React)                  │   │
│  │   Dashboard · Proxy UI · Repeater · Intruder        │   │
│  │   Vulnerabilidades · Red · Utilidades               │   │
│  └──────────────────────┬──────────────────────────────┘   │
│                         │ WebSocket bidireccional           │
│  ┌──────────────────────▼──────────────────────────────┐   │
│  │         P2 — BACKEND (FastAPI + mitmproxy)          │   │
│  │   Proxy HTTP · Repeater · Intruder · Utilidades     │   │
│  │   Sesiones multiusuario · PAC · WebSockets          │   │
│  └────────┬──────────────┬──────────────┬──────────────┘   │
│           │              │              │                   │
│  ┌────────▼──────┐ ┌─────▼───────┐ ┌───▼────────────────┐ │
│  │ P3 PLAYWRIGHT │ │  P5 — IA    │ │  P4 — DEVTOOLS     │ │
│  │  Spider       │ │  Claude API │ │  CDP Client        │ │
│  │  Forms        │ │  Prompts    │ │  Network Analyzer  │ │
│  │  Attacker     │ │  Classifier │ │  Console Analyzer  │ │
│  │  Orchestrator │ │  Orchestrat.│ │  Packet Builder    │ │
│  └───────────────┘ └─────────────┘ └────────────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                           │
              ┌────────────▼────────────┐
              │   USUARIO EXTERNO       │
              │  Navegador con PAC      │
              │  configurado            │
              └─────────────────────────┘
```

### Módulos y responsabilidades

#### P1 — Frontend (React 18 + Vite + Tailwind CSS)
La capa de presentación. Todo lo que el usuario ve y toca. Se comunica exclusivamente con P2 a través de WebSocket. No habla directamente con P3, P4 ni P5.

**Secciones principales:**
- Panel Proxy — peticiones interceptadas en tiempo real
- Repeater — editor y reenvío manual de peticiones
- Intruder — configuración y ejecución de ataques automatizados
- Panel de Vulnerabilidades — alertas detectadas por la IA
- Panel de Red — tráfico capturado por DevTools en tiempo real
- Utilidades — Encoder/Decoder, Hash Generator, Regex Tester, Payload Generator
- Onboarding PAC — asistente de configuración del proxy

#### P2 — Backend (Python 3.11 + FastAPI + mitmproxy + WebSockets)
El núcleo del sistema. Conecta todos los módulos. Es el único que habla con todos los demás.

**Componentes:**
- Servidor FastAPI en puerto 8000
- Proxy TCP real con mitmproxy en puerto 8080
- WebSocket server para comunicación en tiempo real con P1
- Gestión de sesiones multiusuario por token UUID
- Motor de fuzzing asíncrono con asyncio.Semaphore
- Biblioteca de payloads (SQLi, XSS, fuzzing)
- Archivo PAC generado dinámicamente
- Endpoints de utilidades (hash, encode, regex)

#### P3 — Playwright (Python + Playwright 1.44 + asyncio)
El navegador automatizado. Navega, descubre y ataca sin intervención humana.

**Componentes:**
- Spider/crawler con algoritmo BFS
- Form Discoverer con soporte AJAX
- Tech Fingerprinter (9 tecnologías detectables)
- Web Attacker con SQLi y Blind SQLi boolean/time-based
- Orchestrator Receiver (receptor de instrucciones de P5)
- Event Reporter (envío de resultados a P2)

#### P4 — Chrome DevTools (Python + CDP + websockets)
Captura todo el tráfico de red del navegador en tiempo real.

**Componentes:**
- Chrome Launcher (arranca Chrome con --remote-debugging-port=9222)
- CDP Client (cliente WebSocket al Chrome DevTools Protocol)
- Packet Builder (transforma eventos CDP en objetos paquete unificados)
- Network Analyzer (detecta patrones sospechosos, headers ausentes, cookies inseguras)
- Console Analyzer (detecta información sensible en logs: API keys, paths, passwords)
- Packet Reporter (envía paquetes al backend de P2)

#### P5 — IA + GitHub (Python + Anthropic API + GitHub Actions)
El cerebro del sistema y el guardián del repositorio.

**Componentes IA:**
- Cliente Anthropic con reintentos exponenciales
- 4 prompts especializados (paquetes de red, intruder, consola, fingerprint)
- Vulnerability Classifier con umbral de confianza del 60%
- Attack Orchestrator (ciclo completo: fingerprint → spider → ataques → confirmación)

**Componentes GitHub:**
- Estructura del repositorio y CONTRIBUTING.md
- Protección de rama main
- GitHub Actions pipeline de despliegue automático
- Revisión semanal de commits y PRs

### Flujo de datos principal

```
Usuario navega con proxy PAC activo
         ↓
mitmproxy (P2, puerto 8080) intercepta la petición
         ↓
P2 emite evento WebSocket al frontend de P1
P2 envía paquete a P5 para análisis
P2 almacena paquete en sesión
         ↓
P4 (CDP) captura el mismo tráfico desde Chrome
P4 detecta patrones sospechosos
P4 envía paquete estructurado a P2
         ↓
P5 analiza el paquete con Claude API
P5 determina si hay vulnerabilidad (confianza > 60%)
P5 genera instrucción para P3 si procede
         ↓
P3 recibe instrucción, ejecuta el ataque, captura screenshot
P3 devuelve resultado a P5
         ↓
P5 confirma vulnerabilidad (2 confirmaciones adicionales)
P5 clasifica por severidad OWASP y genera ficha completa
P5 emite evento al frontend de P1 via P2
         ↓
P1 muestra alerta en el panel de vulnerabilidades
```

### Infraestructura de despliegue

- **Servidor:** Hetzner Cloud CX22 (2 vCPU, 4GB RAM, ~4€/mes)
- **Sistema operativo:** Ubuntu 24.04 LTS
- **Contenedorización:** Docker + Docker Compose
- **Proxy inverso:** Nginx (enruta /api/ al backend, / al frontend, /ws/ con WebSockets)
- **HTTPS:** Let's Encrypt via Certbot
- **CI/CD:** GitHub Actions (deploy automático en cada push a main)

### Contratos entre módulos

**Formato paquete de red (P4 → P2 → P1/P5):**
```json
{
  "id": "uuid",
  "method": "GET",
  "url": "http://...",
  "status": 200,
  "size": 1024,
  "time": 145,
  "timestamp": "ISO-8601",
  "request_headers": {},
  "request_body": null,
  "response_headers": {},
  "response_body": "...",
  "suspicious": false,
  "vulnerable": false
}
```

**Formato instrucción IA (P5 → P3):**
```json
{
  "type": "attack",
  "url": "http://objetivo.com/pagina",
  "selector": "input[name='id']",
  "payload": "' OR '1'='1",
  "verify": "admin",
  "session_token": "uuid"
}
```

**Formato evento WebSocket (P2 → P1):**
```json
{
  "type": "request_intercepted | intruder_result | vulnerability_detected | network_packet",
  "payload": { ... }
}
```

## Impacto
La arquitectura técnica es el documento de referencia para entender cómo funciona el sistema completo. Es obligatorio incluirlo en el informe PDF de la práctica.
