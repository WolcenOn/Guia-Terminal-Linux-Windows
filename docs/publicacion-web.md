# Publicar la guía como página web

Esta guía está preparada para publicarse como una web de documentación usando MkDocs y GitHub Pages.

---

## 1. Qué se ha añadido

- `mkdocs.yml`: configuración de la web y del menú lateral.
- `docs/index.md`: portada pedagógica de la web.
- `docs/itinerarios.md`: rutas de aprendizaje.
- `docs/guia-docente.md`: orientación para usar la guía en clase.
- `docs/actividades-interactivas.md`: actividades con desplegables, checklists y autoevaluación.
- `.github/workflows/deploy-docs.yml`: flujo automático para publicar la web.

---

## 2. Activar GitHub Pages

En el repositorio:

1. Ir a `Settings`.
2. Entrar en `Pages`.
3. En `Build and deployment`, elegir `GitHub Actions`.
4. Guardar los cambios.
5. Ir a la pestaña `Actions`.
6. Ejecutar o esperar el workflow `Publicar documentación`.

---

## 3. Resultado esperado

Cuando termine correctamente, GitHub Pages mostrará una URL parecida a:

```text
https://wolcenon.github.io/Guia-Terminal-Linux-Windows/
```

Desde ahí se verá una web con:

- Menú lateral.
- Buscador.
- Navegación por secciones.
- Código con botón de copia.
- Bloques desplegables.
- Checklists.
- Avisos y notas didácticas.

---

## 4. Diferencia entre README y web

| Vista | Uso |
|---|---|
| README del repositorio | Portada técnica dentro de GitHub |
| GitHub Pages | Web pedagógica navegable |
| MkDocs | Sistema que convierte Markdown en documentación web |

---

## 5. Mantenimiento

Para añadir nuevos temas:

1. Crear archivo Markdown dentro de `docs/`.
2. Añadirlo al menú en `mkdocs.yml`.
3. Hacer commit y push.
4. GitHub Actions reconstruirá la web.

---

## 6. Recomendación pedagógica

La web debe priorizar:

- Rutas claras.
- Explicaciones breves.
- Prácticas guiadas.
- Checklists.
- Actividades con solución desplegable.
- Proyectos integradores.
