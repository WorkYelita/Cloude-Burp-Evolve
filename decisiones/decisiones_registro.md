---
fecha: 2026-05-02
tipo: Decisión
proyecto: HookSuite
---

# HookSuite — Registro de decisiones

## Contexto
Registro cronológico de todas las decisiones tomadas durante el proyecto con su justificación.

## Contenido

### Decisión 01 — Línea de trabajo: Red Team
**Fecha:** Inicio del proyecto
**Decisión:** Construir una herramienta de Red Team (pentesting web) en vez de Blue Team o Normativa.
**Motivo:** La propuesta del profesor Carlos encajaba directamente con esta línea. Es la más técnicamente ambiciosa y la que mejor demuestra las capacidades del equipo.

---

### Decisión 02 — Arquitectura: WebSockets + backend en Hetzner
**Fecha:** Fase de investigación
**Decisión:** El proxy interceptor corre en el backend del servidor Hetzner, no en el navegador.
**Motivo:** El modelo de seguridad del navegador impide interceptar tráfico de otras pestañas, actuar como proxy TCP o modificar headers protegidos. Mover la lógica al backend resuelve estas tres limitaciones de golpe. Investigación realizada por Chema y Carlos (trabajadores) y validada contra el referente Caido.

---

### Decisión 03 — Solución para el proxy: archivo PAC
**Fecha:** Fase de investigación
**Decisión:** Usar un archivo PAC (Proxy Auto-Configuration) para que el navegador del usuario enrute el tráfico a través del servidor.
**Motivo:** Es la opción con menos fricción para el usuario que no requiere instalar nada. Compatible con todos los navegadores modernos. Es el techo técnico posible sin instalar una extensión.
**Descartadas:** Extensión de navegador, certificado CA propio, proxy SOCKS5, enfoque híbrido Electron.

---

### Decisión 04 — Nombre del proyecto: HookSuite
**Fecha:** 2026-05-02
**Decisión:** El proyecto se llama HookSuite.
**Motivo:** "Hook" evoca interceptación y captura de tráfico. "Suite" indica colección de módulos. Guiño directo a Burp Suite sin copiar el nombre. Elegido entre 5 opciones propuestas (WebRecon, Intercepta, PwnProxy, NullByte, HookSuite).

---

### Decisión 05 — P5 asumido por el responsable del proyecto
**Fecha:** 2026-05-02
**Decisión:** El rol de P5 (IA + GitHub) lo asume el responsable del proyecto, no un trabajador.
**Motivo:** P5 es el rol con más visión transversal. Tener el control del repositorio, del informe PDF y del módulo de IA permite supervisar el estado real del proyecto en todo momento sin depender de nadie.

---

### Decisión 06 — Repositorio bajo organización FeetLovers
**Fecha:** 2026-05-02
**Decisión:** Transferir el repositorio de la cuenta personal de WorkYelita a la organización GitHub FeetLovers.
**Motivo:** Los repositorios personales no permiten gestionar roles y permisos diferenciados entre colaboradores. La organización permite asignar roles Owner/Admin/Write/Read correctamente.

---

### Decisión 07 — Desarrollo en paralelo por módulos
**Fecha:** Planificación del proyecto
**Decisión:** Cada miembro desarrolla su módulo de forma independiente con contratos de integración definidos desde el día 1.
**Motivo:** El equipo trabaja con horarios flexibles y desde casa. El desarrollo en paralelo permite autonomía total. Los contratos entre módulos evitan que la integración se convierta en un caos en la semana 3.

---

### Decisión 08 — Informe PDF con Typst
**Fecha:** Planificación del proyecto
**Decisión:** El informe PDF se maqueta con Typst en vez de Word o LaTeX.
**Motivo:** Typst tiene curva de aprendizaje baja, sintaxis similar a Markdown y produce PDFs de calidad profesional. Es más rápido que LaTeX y produce mejor resultado que Word.

---

### Decisión 09 — Optimización de Playwright: page.fill() en vez de page.type()
**Fecha:** Planificación del proyecto
**Decisión:** Usar siempre `page.fill()` en vez de `page.type()` en todos los scripts de Playwright.
**Motivo:** Indicación directa del profesor Carlos. `page.fill()` pasa el texto completo al campo de una vez en vez de simular pulsación tecla a tecla. Mejora de velocidad medida: x60 aproximadamente.

---

### Decisión 10 — Entorno de pruebas: DVWA
**Fecha:** Planificación del proyecto
**Decisión:** Usar DVWA (Damn Vulnerable Web Application) en Docker como entorno de pruebas para todos los módulos.
**Motivo:** Aplicación web deliberadamente vulnerable diseñada para practicar pentesting. Nunca probar contra webs reales sin autorización expresa.

## Impacto
Este registro permite tener trazabilidad de por qué el proyecto es como es y justificar las decisiones ante el profesor en la presentación oral.
