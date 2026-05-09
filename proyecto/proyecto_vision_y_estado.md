---
fecha: 2026-05-09
tipo: Avance
proyecto: HookSuite
---

# HookSuite — Visión, objetivos y estado actual

## Contexto
Documento principal del proyecto HookSuite. Recoge la visión inicial, los objetivos, las decisiones estructurales tomadas y el estado actual del desarrollo.

## Contenido

### Qué es HookSuite
HookSuite es una herramienta de auditoría de seguridad web que combina interceptación de tráfico HTTP en tiempo real, automatización de ataques con Playwright y análisis con inteligencia artificial para detectar vulnerabilidades de forma automatizada. Funcionalmente es similar a Burp Suite pero construida desde cero como aplicación web accesible desde el navegador.

### Contexto académico
Práctica 1 del Módulo de Ciberseguridad Avanzada, Curso 2026. Grupos de 1 a 5 personas. Entrega: 25 de Mayo de 2026. Presentación oral de 10 minutos en vivo demostrando la herramienta funcionando.

### Demo intermedia acordada
El equipo ha acordado presentar una demo al profesor el **miércoles 13 de Mayo**. El equipo trabaja el fin de semana y lunes/martes para llegar con el sistema integrado.

### Línea de trabajo elegida
Red Team — Escáner de vulnerabilidades web con IA (opción 03 del enunciado).

### Arquitectura técnica definitiva

```
Usuario (navegador con proxy PAC)
         ↓
P1 — Frontend React (dashboard)
         ↓ WebSocket
P2 — Backend FastAPI + mitmproxy (proxy HTTP real)
    ↓              ↓              ↓
P3 Playwright   P5 IA Claude   P4 DevTools CDP
(automatización) (análisis)    (captura red)
```

### Stack tecnológico
- Frontend: React 18 + Vite + Tailwind CSS
- Backend: Python 3.11 + FastAPI + mitmproxy + WebSockets
- Automatización: Playwright + asyncio
- Captura de red: Chrome DevTools Protocol (CDP)
- Inteligencia Artificial: Anthropic Claude API (claude-sonnet-4-20250514)
- Infraestructura: Docker + Hetzner Cloud CX22 + Nginx + GitHub Actions

### Repositorio
- Organización GitHub: Feet-Lovers (con guión)
- Repositorio: Feet-Lovers/Proyecto-Evolve
- Rama principal: main (protegida)

### Entregables de la práctica
1. URL de la herramienta desplegada en Hetzner (accesible en el momento de la evaluación)
2. URL del repositorio GitHub con todo el código y commits del desarrollo
3. Informe de documentación en formato PDF (entregado en el campus virtual)
4. Presentación oral de 10 minutos demostrando la herramienta en vivo

### Criterios de evaluación
| Criterio | Peso |
|----------|------|
| Funcionalidad y calidad técnica | 30% |
| Dashboard web y usabilidad | 15% |
| Despliegue correcto en Hetzner | 15% |
| Calidad del repositorio GitHub | 10% |
| Calidad del informe PDF | 20% |
| Road map de mejora Práctica 2 | 10% |

### Estado actual — 9 de Mayo 2026

| Rol | Nombre | Usuario GitHub | Commits | Último push | Avance estimado | Estado |
|-----|--------|---------------|---------|-------------|----------------|--------|
| P1 — Frontend | Ivan Medina Castro | imeca | 2+ | 7 Mayo | Bloques iniciales | 🔴 Trabajando fin de semana |
| P2 — Backend | Macarena Rogerio | WorkYelita | 18+ | 6 Mayo | Bloques 01-05 | 🟡 Trabajando fin de semana |
| P3 — Playwright | Nacho García Monge | Numial | 8+ | 7 Mayo | Bloques 01-05 | ✅ Trabajando fin de semana |
| P4 — DevTools | Carlos Bañuelos Fernández | OataaOlaf | 10+ | 8 Mayo | Módulo completo | ✅ Completo |
| P5 — IA + GitHub | Jose María López Ausín | JoSeMhack | 16 | 9 Mayo | Bloques 01-03 + infra | 🟡 En espera de integración |

### Bloque 01 de P5 — Estado detallado
| Paso | Tarea | Estado |
|------|-------|--------|
| Paso 1 | Crear y estructurar el repositorio | ✅ |
| Paso 2 | Crear las ramas de trabajo | ✅ |
| Paso 3 | Protección de rama main | ✅ |
| Paso 4 | Pipeline GitHub Actions `deploy.yml` | 🟡 Creado — esperando secrets |
| Paso 5 | Rutina de revisión semanal | 🔄 Activa |

### Infraestructura del repositorio — Estado
| Elemento | Estado |
|----------|--------|
| Rama `develop` | ✅ Eliminada |
| Carpeta `docs/` en main | ✅ Creada |
| `docs/manual_ia.md` | ✅ Subido |
| `docs/capturas/` (5 subcarpetas) | ✅ Creadas con `.gitkeep` |
| Pipeline `deploy.yml` | 🟡 Listo — esperando IP Hetzner |
| Secrets GitHub Actions | ⏳ Pendiente — esperando IP de Macarena |

### Alertas activas
- 🔴 Demo el miércoles 13 de Mayo — equipo trabajando fin de semana
- 🟡 Pipeline bloqueado — esperando IP Hetzner de Macarena
- 🟡 Endpoint `POST /api/playwright/instruction/{token}` pendiente en Macarena — bloquea integración IA-Playwright
- 🟡 Endpoint `POST /api/vulnerabilities` pendiente en Macarena
- 🟡 P1, P2 y P3 sin convención de commits — penaliza el 10% de la nota
- ⚠️ Archivo `devtools/re` con 130.159 líneas — pendiente que Carlos lo elimine
- ⚠️ Dos PRs mergeados a main — pendiente de revisar quién los aprobó y qué contienen
- ⚠️ Profesor pendiente de añadir como colaborador del repositorio
- ⚠️ Respuesta del equipo sobre modo silencioso en Práctica 1 — pendiente

### Contrato de integración — Estado actual
| Integración | Endpoint | Estado |
|-------------|----------|--------|
| P4 → P2 (paquetes de red) | `POST /api/network/packet` | ✅ Macarena implementó el endpoint |
| P5 → P2 → P3 (instrucciones) | `POST /api/playwright/instruction/{token}` | ❌ Macarena pendiente |
| P2 → P5 (respuesta de ataque) | `{vulnerable, response_body, status, time_ms}` | 🟡 P5 listo con mock |
| P5 → P2 (vulnerabilidades) | `POST /api/vulnerabilities` | ❌ Macarena pendiente |

### Análisis técnico abierto
- Capacidades de sigilo para pentesting profesional analizadas — documento generado en `conocimiento/`
- Decisión del equipo sobre implementación en Práctica 1 o Práctica 2 pendiente

## Impacto
Este documento es la referencia principal del proyecto. Quedan 16 días para la entrega del 25 de Mayo. Demo intermedia acordada para el miércoles 13 de Mayo.
