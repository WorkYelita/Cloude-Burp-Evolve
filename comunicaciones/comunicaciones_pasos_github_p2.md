# HookSuite — Pasos a seguir en GitHub
**Para:** P2 — Administradora del repositorio  
**Fecha:** 1 de Mayo de 2026

Estos son los cambios que necesito que hagas en el repositorio. Están ordenados por urgencia. Hazlos en este orden exacto.

---

## PASO 1 — Cambiar la rama por defecto de `develop` a `main`

1. Ve a **Settings** del repositorio (pestaña superior derecha)
2. En el menú lateral haz clic en **Branches**
3. En la sección "Default branch" verás que pone `develop`
4. Haz clic en el icono de los dos flechas (switch) que hay a la derecha
5. Selecciona `main` en el desplegable
6. Haz clic en **Update**
7. Confirma el cambio cuando te lo pida

**Por qué:** Toda la estructura del proyecto, el pipeline de despliegue y el manual apuntan a `main` como rama principal. Tener `develop` como default genera confusión al equipo.

---

## PASO 2 — Subir el README.md a main

1. Ve a la rama `main` del repositorio
2. Haz clic en **Add file → Upload files**
3. Sube el archivo `README.md` que te he pasado
4. En el campo de commit message escribe exactamente:
   ```
   docs(infra): añadir README profesional del proyecto
   ```
5. Selecciona **Commit directly to the `main` branch**
6. Haz clic en **Commit changes**

---

## PASO 3 — Subir el CONTRIBUTING.md a main

1. Ve a la rama `main` del repositorio
2. Haz clic en **Add file → Upload files**
3. Sube el archivo `CONTRIBUTING.md` que te he pasado
4. En el campo de commit message escribe exactamente:
   ```
   docs(infra): añadir guía de contribución y convención de commits
   ```
5. Selecciona **Commit directly to the `main` branch**
6. Haz clic en **Commit changes**

---

## PASO 4 — Añadirme como administrador del repositorio

Necesito permisos de administrador para poder gestionar el repositorio correctamente desde mi rol de P5.

1. Ve a **Settings** del repositorio
2. En el menú lateral haz clic en **Collaborators and teams**
3. Busca mi usuario de GitHub en la lista de colaboradores actuales
4. Cambia mi rol de **Write** a **Admin**
5. Guarda los cambios

---

## PASO 5 — Renombrar las ramas con mayúsculas

Las ramas `feature/Backend`, `feature/Playwright` y `feature/Frontend` tienen la primera letra en mayúscula. La convención del proyecto define minúsculas. Hay que renombrarlas.

**Para renombrar una rama en GitHub:**

1. Ve a la lista de ramas del repositorio
2. Busca la rama `feature/Backend`
3. Haz clic en los tres puntos `...` que aparecen a la derecha
4. Selecciona **Rename branch**
5. Escribe el nuevo nombre: `feature/backend` (todo en minúsculas)
6. Haz clic en **Rename branch**

Repite el mismo proceso para:
- `feature/Playwright` → `feature/playwright`
- `feature/Frontend` → `feature/frontend`

**Aviso importante:** Después de renombrar, los miembros que ya tienen la rama clonada en local necesitan actualizar su referencia local. Diles que ejecuten este comando en su terminal:
```bash
git branch -m feature/Backend feature/backend
git fetch origin
git branch -u origin/feature/backend feature/backend
```

---

## PASO 6 — Eliminar la rama `develop`

Una vez que `main` sea la rama por defecto (Paso 1), la rama `develop` ya no tiene utilidad y genera confusión.

1. Ve a la lista de ramas del repositorio
2. Busca la rama `develop`
3. Haz clic en el icono de la papelera que aparece a la derecha
4. Confirma la eliminación

---

## PASO 7 — Aplicar la convención de commits desde hoy

A partir de hoy todos tus commits en `feature/backend` deben seguir el formato del CONTRIBUTING.md que te he pasado. El formato es:

```
tipo(scope): descripción en imperativo presente
```

Ejemplos para tu módulo:
```
feat(backend): implementar endpoint de reenvío del repeater
fix(backend): corregir gestión de sesiones WebSocket
chore(backend): actualizar requirements.txt con nueva dependencia
docs(backend): documentar endpoints en Swagger
```

Los commits anteriores no los toques. Lo pasado está y reescribir el historial ahora haría más daño que bien. Aplica la convención solo a los commits nuevos.

---

## Resumen de lo que necesito

| Paso | Acción | Urgencia |
|------|--------|----------|
| 1 | Cambiar rama default de `develop` a `main` | 🔴 Alta |
| 2 | Subir README.md a main | 🔴 Alta |
| 3 | Subir CONTRIBUTING.md a main | 🔴 Alta |
| 4 | Darme permisos de administrador | 🔴 Alta |
| 5 | Renombrar ramas con mayúsculas | 🟡 Media |
| 6 | Eliminar rama `develop` | 🟡 Media |
| 7 | Aplicar convención de commits desde hoy | 🔴 Alta |

Cuando hayas terminado dímelo para verificar que todo está correcto.

---

*Instrucciones de P5 para P2 — Proyecto HookSuite — Mayo 2026*
