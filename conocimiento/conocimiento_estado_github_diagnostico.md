---
fecha: 2026-05-02
tipo: Conocimiento
proyecto: HookSuite
---

# HookSuite — Diagnóstico y configuración del repositorio GitHub

## Contexto
Registro del estado inicial del repositorio cuando fue creado por P2, los problemas detectados y todas las acciones correctivas realizadas el 2 de Mayo de 2026.

## Contenido

### Estado inicial del repositorio (creado por P2 — WorkYelita)

**Repositorio original:** github.com/WorkYelita/Proyecto-Evolve (cuenta personal)

**Problemas detectados:**

| # | Problema | Impacto |
|---|---------|---------|
| 1 | Rama por defecto era `develop` en vez de `main` | Alto — confusión en el equipo y en el pipeline |
| 2 | Ramas con mayúsculas (feature/Backend, feature/Playwright, feature/Frontend, feature/IA) | Medio — inconsistencia con la convención |
| 3 | Commits de P2 sin convención (ej: "no va el gitignore shit") | Alto — penaliza el 10% de la nota |
| 4 | Sin CONTRIBUTING.md ni README profesional | Alto — el equipo trabaja sin reglas escritas |
| 5 | Repositorio en cuenta personal — sin gestión de roles | Alto — no se pueden asignar permisos diferenciados |

**Estado de las ramas en el momento del diagnóstico:**
- `develop` — Default, 1 commit
- `feature/Backend` — 13 commits (P2 trabajando activamente)
- `feature/devtools` — 7 commits (P4 trabajando activamente)
- `main` — 0 commits (existía pero vacía)
- `feature/Playwright` — 0 commits
- `feature/IA` — 0 commits
- `feature/Frontend` — 0 commits

### Acciones correctivas realizadas (2 de Mayo de 2026)

**Acción 1 — Creación de organización GitHub**
Se creó la organización `FeetLovers` en GitHub para poder gestionar roles y permisos correctamente.

**Acción 2 — Transferencia del repositorio**
El repositorio se transfirió de `WorkYelita/Proyecto-Evolve` a `FeetLovers/Proyecto-Evolve`. Todo el contenido (ramas, commits, archivos) se mantuvo intacto. GitHub crea redirección automática de la URL antigua a la nueva.

**Acción 3 — Permisos de administrador para P5**
P5 (responsable del proyecto) recibió permisos de Admin en el repositorio dentro de la organización.

**Acción 4 — Cambio de rama por defecto**
La rama por defecto se cambió de `develop` a `main` desde Settings → General.

**Acción 5 — Subida de README.md y CONTRIBUTING.md**
Ambos archivos se subieron directamente a la rama `main` con los commits:
- `docs(infra): añadir README profesional del proyecto`
- `docs(infra): añadir guía de contribución y convención de commits`

**Acción 6 — Renombrado de ramas a minúsculas**
- `feature/Backend` → `feature/backend`
- `feature/Playwright` → `feature/playwright`
- `feature/Frontend` → `feature/frontend`
- `feature/IA` → `feature/ia`

**Acción 7 — Protección de rama main**
Regla de protección activada en Settings → Branches:
- Require a pull request before merging ✅
- Require approvals: 1 ✅
- Dismiss stale pull request approvals ✅

**Acción 8 — Actualización de repos locales de P2 y P4**
P2 y P4 ejecutaron los comandos para actualizar la URL remota a la nueva organización:
```bash
git remote set-url origin https://github.com/FeetLovers/Proyecto-Evolve.git
git fetch origin
```

### Estado del repositorio tras las correcciones

| Aspecto | Estado |
|---------|--------|
| Organización | FeetLovers ✅ |
| Rama por defecto | main ✅ |
| README.md | Profesional en main ✅ |
| CONTRIBUTING.md | En main con convención de commits ✅ |
| Ramas de módulo | 5 ramas en minúsculas ✅ |
| Protección de main | Activada, requiere PR y aprobación ✅ |
| Permisos P5 | Admin ✅ |
| P2 y P4 en local | Actualizados a nueva URL ✅ |

### Pendiente
- Pipeline GitHub Actions `.github/workflows/deploy.yml` — pendiente de crear cuando P2 proporcione la IP del servidor Hetzner
- P2 debe aplicar la convención de commits en todos los commits futuros

### Valoración del trabajo de cada rol en GitHub

**P2 — WorkYelita:** Tomó la iniciativa de crear el repositorio antes de recibir instrucciones. Muy proactiva. Sus commits iniciales no siguen la convención pero está comprometida a aplicarla desde ahora. Ha completado Bloques 01-02 del backend.

**P4 — OataaOlaf:** Sigue la convención de commits casi perfectamente desde el primer commit. Es el miembro más disciplinado del equipo en cuanto a GitHub. Ha completado Bloques 01-02-03 del módulo DevTools.

## Impacto
Este registro documenta la evolución del repositorio y justifica las decisiones de configuración tomadas.
