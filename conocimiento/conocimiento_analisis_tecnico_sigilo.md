---
fecha: 2026-05-09
tipo: Conocimiento
proyecto: HookSuite
---

# HookSuite — Análisis técnico interno: Capacidades de sigilo para pentesting profesional

## Contexto

Análisis interno generado el 9 de Mayo de 2026 para que el equipo evalúe el esfuerzo de implementar capacidades de operación sigilosa en HookSuite. El enfoque es **pentesting profesional con autorización explícita del cliente**, alineado con el estándar del sector (PTES, OWASP Testing Guide).

Este documento no es una guía de implementación. Es una evaluación de complejidad, impacto en el código actual y estimación de esfuerzo por módulo para que el equipo decida si incluirlo en la Práctica 2.

---

## Qué significa operar de forma sigilosa

En un contexto de auditoría profesional, "sigilo" tiene dos dimensiones distintas que hay que tratar por separado:

**Dimensión 1 — Reducción de ruido en tráfico (punto 2)**
Evitar que los sistemas de detección de la empresa auditada (WAF, IDS, SIEM) identifiquen los ataques como tráfico automatizado o malicioso durante la auditoría.

**Dimensión 2 — Anonimización del origen (punto 4)**
Ocultar o enmascarar la IP y la huella del dispositivo desde el que opera la herramienta.

Ambas dimensiones son independientes y tienen complejidades distintas. Se analizan por separado.

---

## DIMENSIÓN 1 — Reducción de ruido en tráfico

### Estado actual de HookSuite

| Componente | Comportamiento actual | Nivel de ruido |
|------------|----------------------|----------------|
| Intruder | 5 peticiones paralelas con payloads SQLi/XSS en crudo | 🔴 Alto |
| Repeater | Petición única manual | 🟢 Bajo |
| Proxy mitmproxy | Interceptación pasiva | 🟢 Bajo |
| Playwright | Navegación automatizada con timings predecibles | 🟡 Medio |
| CDP (DevTools) | Captura local, no genera tráfico externo | 🟢 Bajo |

### Técnicas de reducción de ruido — análisis por técnica

---

#### Técnica 1 — Throttling y delays aleatorios en el Intruder

**Qué hace:** Introduce pausas aleatorias entre peticiones para imitar comportamiento humano.

**Dónde impacta:** Módulo de P2 — motor de fuzzing (`intruder_service.py`).

**Cambios necesarios:**
- Añadir parámetro `delay_min` y `delay_max` al modelo de configuración de ataque
- Introducir `asyncio.sleep(random.uniform(delay_min, delay_max))` entre peticiones
- Reducir el `asyncio.Semaphore` de 5 a 1-2 para ataques silenciosos
- Exponer estos parámetros en la UI de P1 como "Modo silencioso"

**Complejidad:** 🟢 Baja — cambios localizados en 2-3 archivos de P2 y 1 componente de P1.

**Impacto en la demo:** El ataque tarda más. Para la demo con DVWA usar siempre modo rápido.

---

#### Técnica 2 — Rotación de User-Agent

**Qué hace:** Cambia el header `User-Agent` en cada petición para evitar que el WAF detecte un patrón de agente automatizado.

**Dónde impacta:** Módulo de P2 — proxy HTTP y motor de fuzzing.

**Cambios necesarios:**
- Crear una biblioteca de User-Agents reales (Chrome, Firefox, Safari en distintas versiones y SO)
- Aplicar rotación aleatoria en cada petición del Intruder y del Repeater
- Opcionalmente exponer esto como configuración en P1

**Complejidad:** 🟢 Baja — implementación de 20-30 líneas en un módulo de utilidades de P2.

---

#### Técnica 3 — Fragmentación y codificación de payloads

**Qué hace:** Transforma los payloads de ataque para que no coincidan con las firmas conocidas de los WAFs (por ejemplo, escribir `' OR '1'='1` de formas alternativas que el motor SQL interpreta igual pero el WAF no reconoce).

**Dónde impacta:** Módulo de P2 — biblioteca de payloads. Módulo de P5 — generación de instrucciones de ataque.

**Técnicas concretas:**
- Codificación URL doble: `%2527` en vez de `'`
- Comentarios SQL inline: `'/**/OR/**/1=1`
- Mayúsculas/minúsculas alternadas: `SeLeCt` en vez de `SELECT`
- Codificación hexadecimal de strings
- Uso de funciones equivalentes: `CONCAT()` en vez de `||`

**Cambios necesarios:**
- Crear un módulo `payload_encoder.py` en P2 con las transformaciones
- Integrar el encoder en el pipeline del Intruder como capa opcional
- P5 puede usar Claude para generar variantes de payloads adaptadas al target

**Complejidad:** 🟡 Media — requiere investigación de técnicas de bypass específicas por tipo de vulnerabilidad y WAF objetivo.

---

#### Técnica 4 — Humanización del comportamiento de Playwright

**Qué hace:** Hace que la navegación automatizada de Playwright imite el comportamiento de un usuario humano real.

**Dónde impacta:** Módulo de P3 — todos los módulos de automatización.

**Cambios necesarios:**
- Movimientos de ratón con trayectorias curvas (no lineales)
- Scroll aleatorio antes de interactuar con elementos
- Tiempos de escritura variables (aunque se use `page.fill()`, el click previo puede tener delay)
- Resoluciones de pantalla y viewports variables
- Desactivar las señales que delatan a Playwright (`navigator.webdriver = false`)

**Complejidad:** 🟡 Media — Playwright tiene APIs para parte de esto. La desactivación del `webdriver` flag requiere un script de inicialización específico.

**Nota importante:** Playwright-Extra con el plugin `stealth` resuelve gran parte de esto con una sola dependencia. Vale la pena evaluarlo.

---

#### Técnica 5 — Distribución temporal del ataque

**Qué hace:** En vez de lanzar todos los ataques en una sesión, distribuirlos a lo largo de horas o días para evitar umbrales de alerta por volumen.

**Dónde impacta:** Arquitectura general — requiere persistencia de estado entre sesiones.

**Cambios necesarios:**
- Sistema de cola de ataques persistente (Redis o SQLite)
- Scheduler para ejecutar ataques en ventanas horarias configurables
- Panel en P1 para gestionar la cola y programar ataques

**Complejidad:** 🔴 Alta — requiere cambios arquitecturales significativos. Las sesiones actualmente son en memoria. Habría que migrar a persistencia.

**Recomendación:** Reservar para Práctica 2 o versión posterior.

---

### Resumen de complejidad — Dimensión 1

| Técnica | Complejidad | Módulos afectados | Recomendación |
|---------|-------------|-------------------|---------------|
| Throttling y delays | 🟢 Baja | P2, P1 | Práctica 2 — fácil de implementar |
| Rotación User-Agent | 🟢 Baja | P2 | Práctica 2 — fácil de implementar |
| Fragmentación payloads | 🟡 Media | P2, P5 | Práctica 2 — requiere investigación |
| Humanización Playwright | 🟡 Media | P3 | Práctica 2 — evaluar playwright-extra |
| Distribución temporal | 🔴 Alta | P1, P2, infra | Versión futura |

---

## DIMENSIÓN 2 — Anonimización del origen

### Estado actual de HookSuite

Toda la actividad de HookSuite sale desde la IP pública del servidor Hetzner. Esa IP es visible en los logs de cualquier sistema auditado y es directamente atribuible al servidor del cliente o del equipo auditor.

### Técnicas de anonimización — análisis por técnica

---

#### Técnica 1 — Integración con red Tor

**Qué hace:** Enruta el tráfico de ataque a través de la red Tor para ocultar la IP de origen.

**Dónde impacta:** Módulo de P2 — cliente HTTP del Intruder y del Repeater.

**Cambios necesarios:**
- Instalar `tor` en el servidor Hetzner y en el Docker Compose
- Configurar `httpx` para usar el proxy SOCKS5 de Tor (`socks5://127.0.0.1:9050`)
- Añadir opción en la UI de P1 para activar/desactivar el enrutamiento por Tor
- Implementar rotación de circuitos Tor entre sesiones de ataque

**Limitaciones importantes:**
- Tor introduce latencia significativa (2-10 segundos por petición)
- Algunos sistemas bloquean activamente los nodos de salida de Tor
- No es compatible con WebSockets (afecta a la comunicación en tiempo real)
- El Blind SQLi time-based pierde fiabilidad con la latencia de Tor

**Complejidad:** 🟡 Media — la integración técnica es manejable pero las limitaciones de latencia afectan a funcionalidades core.

---

#### Técnica 2 — Pool de proxies rotatorios

**Qué hace:** Distribuye las peticiones de ataque a través de múltiples IPs de proxies externos, rotando entre ellas para que ninguna IP acumule suficiente volumen como para activar alertas.

**Dónde impacta:** Módulo de P2 — cliente HTTP. Infraestructura — requiere acceso a un pool de proxies.

**Cambios necesarios:**
- Integrar un cliente de proxy rotatorio (servicios como BrightData, Oxylabs, o proxies propios en VPS adicionales)
- Lógica de rotación en el motor de fuzzing de P2
- Gestión de proxies fallidos y reintentos
- Panel de configuración en P1

**Limitaciones:**
- Los proxies de calidad tienen coste mensual (50-200€/mes para uso profesional)
- Los proxies gratuitos son inestables y frecuentemente bloqueados
- Aumenta significativamente la complejidad de la infraestructura

**Complejidad:** 🔴 Alta — dependencia de infraestructura externa con coste económico.

---

#### Técnica 3 — Múltiples VPS como nodos de ataque

**Qué hace:** En vez de lanzar todos los ataques desde el servidor Hetzner principal, distribuirlos entre varios VPS temporales que se crean para cada auditoría y se destruyen al terminar.

**Dónde impacta:** Arquitectura completa — requiere un sistema de orquestación de nodos.

**Cambios necesarios:**
- API de orquestación que distribuya ataques entre nodos
- Integración con la API de Hetzner (o DigitalOcean, Vultr) para crear/destruir VPS dinámicamente
- Módulo de P5 para coordinar qué nodo ejecuta qué ataque
- Agregación de resultados en el nodo principal

**Complejidad:** 🔴 Muy alta — es un cambio arquitectural completo. Esencialmente convierte HookSuite en un sistema distribuido.

---

#### Técnica 4 — Spoofing de headers de identificación

**Qué hace:** Falsifica los headers que revelan información sobre el origen de las peticiones: `X-Forwarded-For`, `X-Real-IP`, `Via`, `Referer`.

**Dónde impacta:** Módulo de P2 — todas las peticiones salientes.

**Cambios necesarios:**
- Añadir headers falsos a todas las peticiones del Intruder y Repeater
- Generar IPs de origen falsas aleatorias o configurables
- Rotar los valores entre peticiones

**Limitaciones importantes:**
- Solo funciona si el servidor destino confía ciegamente en estos headers
- Los sistemas bien configurados ignoran o registran `X-Forwarded-For` de fuentes no confiables
- No oculta la IP real a nivel TCP — solo a nivel de aplicación
- Eficacia limitada contra sistemas modernos bien configurados

**Complejidad:** 🟢 Baja — técnicamente simple, pero la eficacia real es limitada.

---

### Resumen de complejidad — Dimensión 2

| Técnica | Complejidad | Coste adicional | Eficacia real | Recomendación |
|---------|-------------|-----------------|---------------|---------------|
| Integración Tor | 🟡 Media | Ninguno | Media | Práctica 2 |
| Pool de proxies rotatorios | 🔴 Alta | 50-200€/mes | Alta | Versión futura |
| Múltiples VPS dinámicos | 🔴 Muy alta | Variable por auditoría | Muy alta | Versión futura |
| Spoofing de headers | 🟢 Baja | Ninguno | Baja | No prioritario |

---

## Valoración global y recomendación para Práctica 2

### Lo que tiene sentido implementar en la Práctica 2

Estas cuatro mejoras tienen buena relación esfuerzo/impacto y no requieren cambios arquitecturales:

1. **Throttling y delays aleatorios** — 2-3 días, P2 + P1
2. **Rotación de User-Agent** — 1 día, P2
3. **Fragmentación de payloads** — 3-4 días, P2 + P5
4. **Humanización de Playwright** (con playwright-extra) — 2-3 días, P3

Estas cuatro juntas convierten a HookSuite en una herramienta significativamente más sigilosa a nivel de capa de aplicación, que es donde la mayoría de WAFs y sistemas de detección operan.

### Lo que requiere más madurez del producto

La anonimización real del origen (Tor, proxies rotatorios, VPS distribuidos) requiere decisiones de infraestructura y posiblemente inversión económica. Son mejoras para una versión más madura del producto, cuando la arquitectura base esté estabilizada y el equipo tenga más contexto sobre los casos de uso reales de los clientes.

### Nota sobre el marco legal y ético

Todas estas capacidades son herramientas estándar en el arsenal de cualquier consultora de pentesting profesional. Su uso legítimo requiere siempre un contrato firmado con el cliente que defina el alcance exacto de la auditoría. HookSuite debería incluir en su UI un aviso explícito de que el uso sin autorización es ilegal, y opcionalmente un campo para registrar el número de contrato o autorización antes de iniciar cualquier auditoría.

---

## Impacto
Este análisis permite al equipo tomar una decisión informada sobre qué capacidades de sigilo incluir en la Práctica 2, con estimaciones reales de esfuerzo y complejidad por módulo.
