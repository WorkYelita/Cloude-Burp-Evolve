---
fecha: 2026-05-02
tipo: Riesgo
proyecto: HookSuite
---

# HookSuite — Mapa de riesgos

## Contexto
Registro de riesgos identificados durante la planificación y seguimiento del proyecto con su estado actual y medidas de mitigación.

## Contenido

### Riesgo 01 — Fallo en la integración de módulos en semana 3
**Probabilidad:** Alta  
**Impacto:** Crítico  
**Estado:** Activo  
**Descripción:** Con 5 módulos desarrollados en paralelo, el momento de integración puede convertirse en el cuello de botella más peligroso del proyecto. Si los módulos no hablan bien entre sí, una semana antes de la entrega el equipo estará apagando fuegos en vez de puliendo la demo.  
**Mitigación:** Contratos entre módulos definidos el día 1 antes de escribir código. Formato JSON acordado entre P2, P4 y P5. Integración progresiva desde la semana 2 en vez de esperar a la semana 3.

---

### Riesgo 02 — P2 como único cuello de botella técnico
**Probabilidad:** Media  
**Impacto:** Crítico  
**Estado:** Activo  
**Descripción:** P2 Backend es el rol que bloquea a todos los demás en distintos momentos. P1 no puede conectar datos reales sin el WebSocket de P2. P4 no puede entregar paquetes sin el endpoint de P2. P5 no puede consumir datos reales sin P2. Si P2 se retrasa, el efecto cascada afecta a todos.  
**Mitigación:** P1, P4 y P5 trabajan con mocks durante las semanas 1 y 2. El cambio de mocks a datos reales es un cambio de una línea, no una refactorización. Monitorizar el avance de P2 semanalmente.

---

### Riesgo 03 — Demo fallida el día de la presentación
**Probabilidad:** Media  
**Impacto:** Alto  
**Estado:** Activo  
**Descripción:** La presentación es en vivo, 10 minutos, demostrando la herramienta funcionando ante el profesor. Si algo falla en el momento crítico, el 45% de la nota (funcionalidad + dashboard + despliegue) se resiente.  
**Mitigación:** El deploy en Hetzner debe estar listo el día 22. Los días 23-25 son solo para pulir y ensayar. Grabar una sesión de backup de la demo funcionando. Ensayar el flujo completo mínimo dos veces antes del día 25.

---

### Riesgo 04 — Archivo PAC con fricción en la demo
**Probabilidad:** Media  
**Impacto:** Medio  
**Estado:** Activo  
**Descripción:** La configuración del PAC requiere un paso manual del usuario. En una demo de 10 minutos ante el profesor, si el proxy no funciona a la primera, el tiempo se consume y la experiencia se degrada.  
**Mitigación:** El importador de peticiones (raw HTTP / cURL) funciona como plan B sin necesidad de configurar el proxy. Tenerlo siempre visible y funcional. Configurar el proxy antes de entrar a la sala de presentación.

---

### Riesgo 05 — Commits sin convención en el historial de GitHub
**Probabilidad:** Alta (ya ocurrió en P2)  
**Impacto:** Medio  
**Estado:** Parcialmente mitigado  
**Descripción:** El historial de commits es un criterio de evaluación explícito (10% de la nota). Commits con mensajes como "no va el gitignore shit" penalizan directamente.  
**Mitigación:** CONTRIBUTING.md subido al repositorio. P2 informada y comprometida a aplicar la convención desde ahora. Revisión semanal del historial por P5 cada viernes.

---

### Riesgo 06 — Playwright con rendimiento lento
**Probabilidad:** Alta sin mitigación  
**Impacto:** Medio  
**Estado:** Mitigado  
**Descripción:** Playwright por defecto simula pulsaciones tecla a tecla. Escribir un texto largo puede tardar hasta 10 segundos.  
**Mitigación:** Usar siempre `page.fill()` en vez de `page.type()`. Mejora de velocidad x60. Implementado desde el inicio en el manual de P3.

---

### Riesgo 07 — Coste de la API de Anthropic
**Probabilidad:** Baja  
**Impacto:** Bajo  
**Estado:** Controlado  
**Descripción:** El módulo de IA hace llamadas a la API de Claude. Un uso intensivo puede generar costes inesperados.  
**Mitigación:** Estimación de ~0.15$ por sesión de auditoría de 30 minutos. Para el desarrollo y las pruebas el coste total estimado es inferior a 5$. Monitorizar el uso desde console.anthropic.com.

---

### Riesgo 08 — Repositorio sin estructura correcta al arrancar P1 y P3
**Probabilidad:** Baja (mitigado)  
**Impacto:** Medio  
**Estado:** Mitigado  
**Descripción:** Si P1 y P3 arrancan antes de que el repositorio tenga la estructura correcta, pueden crear ramas con nombres incorrectos o trabajar en la rama equivocada.  
**Mitigación:** Estructura del repositorio corregida el 2 de Mayo antes de que P1 y P3 arranquen. CONTRIBUTING.md disponible con las reglas exactas.

## Impacto
El mapa de riesgos permite anticipar problemas antes de que ocurran y tener planes de contingencia preparados.
