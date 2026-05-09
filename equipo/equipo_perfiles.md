---
fecha: 2026-05-09
tipo: Avance
proyecto: HookSuite
---

# HookSuite — Perfiles del equipo

## Contexto
Registro de los miembros del equipo, sus roles asignados, usuarios GitHub confirmados y observaciones sobre su forma de trabajar detectadas hasta la fecha.

## Contenido

### Estructura del equipo

| Rol | Nombre completo | Módulo | Usuario GitHub | Email | Estado |
|-----|----------------|--------|---------------|-------|--------|
| P1 | Ivan Medina Castro | Frontend — React + Vite + Tailwind | imeca | medinacastroivan@gmail.com | 🔴 Trabajando fin de semana |
| P2 | Macarena Rogerio | Backend — FastAPI + mitmproxy | WorkYelita | macarenarogerioegea@gmail.com | 🟡 Cuello de botella activo |
| P3 | Nacho García Monge | Playwright — Automatización | Numial | nachogarmo@gmail.com | ✅ Avance sólido |
| P4 | Carlos Bañuelos Fernández | DevTools — Chrome DevTools Protocol | OataaOlaf | charlie_br_wn@hotmail.com | ✅ Módulo completo |
| P5 | Jose María López Ausín | IA + GitHub — Claude API + Gestión repo | JoSeMhack | 20sanchezlopez21@gmail.com | 🟡 En espera de integración |

### Observaciones por miembro

#### P1 — Ivan Medina Castro (imeca)
- Solo 2 commits propios en toda la duración del proyecto
- Último push: 7 de Mayo
- Mensajes de commit sin convención ("correcciones del front", "frontend")
- El commit incluye erratas ("servicesd", "aztualizado") — señal de trabajo apresurado
- Es el miembro más retrasado del equipo y el riesgo más alto para la demo
- Comunicación enviada el 9 de Mayo solicitando aceleración del ritmo
- Comprometido a trabajar el fin de semana para la demo del miércoles

#### P2 — Macarena Rogerio (WorkYelita)
- Creó el repositorio GitHub por iniciativa propia antes de recibir el manual de P5
- Muy proactiva — pasó de 5 a 18 commits entre el 2 y el 6 de Mayo
- Ha implementado: proxy con mitmproxy, repeater, intruder con fuzzing asíncrono, utilidades y endpoint receptor de paquetes de P4
- Sigue sin aplicar la convención de commits después de comprometerse el 2 de Mayo
- Pendiente: IP del servidor Hetzner para desbloquear el pipeline de P5
- Pendiente: endpoint `POST /api/playwright/instruction/{session_token}` — Bloque 06
- Pendiente: endpoint `POST /api/vulnerabilities`
- Solicitud de desbloqueo enviada el 9 de Mayo — respuesta pendiente

#### P3 — Nacho García Monge (Numial)
- Arrancó y tiene avance real y sólido — 8 commits propios
- Ha implementado: base, spider, autenticación, formularios, fingerprinting, automatización de ataque, reporter, receptor de instrucciones de IA y script de demo
- Sin convención de commits
- Último commit es un merge — verificar que el código está en buen estado tras el merge
- Ha abierto al menos un PR mergeado a main — revisar qué contiene
- Comprometido a trabajar el fin de semana para la demo del miércoles

#### P4 — Carlos Bañuelos Fernández (OataaOlaf)
- El miembro más disciplinado del equipo en cuanto a GitHub
- Módulo DevTools aparentemente completo — 10 commits con convención correcta
- Ha documentado el road map de la Práctica 2 con 10 mejoras
- Último push: 8 de Mayo
- Alerta activa: archivo `devtools/re` con 130.159 líneas subido por error en el último commit — pendiente de eliminar
- Comunicación enviada el 9 de Mayo con instrucciones para eliminarlo

#### P5 — Jose María López Ausín (JoSeMhack)
- Primera sesión (2 Mayo): Bloque 02 completo — cliente Anthropic, 4 prompts, clasificador, test standalone
- Segunda sesión (2 Mayo): Bloque 03 completo — orquestador con 3 fases, modo mock, punto de entrada
- Sesión del 9 de Mayo: gestión y documentación — rama develop eliminada, pipeline creado, estructura docs creada, manual_ia.md generado y subido
- 16 commits granulares en feature/ia con convención correcta
- Módulo en espera de integración con Macarena y Nacho para pasar de modo mock a modo real

### Preferencias de trabajo de P5
- Solicitar siempre el fichero completo modificado, nunca fragmentos parciales
- Usar línea de comandos para commits, no GitHub Desktop

### Dinámica del equipo
- P5 actúa como gestor y líder técnico del módulo de IA
- P4 es el referente técnico en cuanto a disciplina de commits
- P2 es el cuello de botella principal — bloquea a P1, P3 y P5 en distintos momentos
- P1 es el riesgo más alto para la demo en este momento
- La comunicación de instrucciones al equipo se realiza a través del responsable del proyecto
- El equipo trabaja el fin de semana + lunes + martes para la demo del miércoles 13 de Mayo

### Contrato de integración — Estado actual

| Integración | Endpoint | Estado |
|-------------|----------|--------|
| P4 → P2 (paquetes de red) | `POST /api/network/packet` | ✅ Macarena implementó el endpoint |
| P5 → P2 → P3 (instrucciones) | `POST /api/playwright/instruction/{token}` | ❌ Macarena pendiente — Bloque 06 |
| P2 → P5 (respuesta de ataque) | `{vulnerable, response_body, status, time_ms}` | 🟡 P5 listo con mock |
| P5 → P2 (vulnerabilidades) | `POST /api/vulnerabilities` | ❌ Macarena pendiente |

### Nota técnica — Campo suspicious
Macarena usa `suspicious: bool` en `NetworkPacket`. P5 usa `suspicious_reasons: list` internamente. Son campos distintos sin conflicto. En semana 3 se puede aprovechar `suspicious: bool` como señal adicional en el clasificador.

## Impacto
Los perfiles del equipo informan las decisiones de gestión, asignación de tareas y seguimiento del progreso.
