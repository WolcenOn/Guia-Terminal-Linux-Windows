# 14 - Git y GitHub para administración de sistemas

Git no solo sirve para programadores. En administración de sistemas permite versionar scripts, documentación, configuraciones, procedimientos y cambios importantes.

---

## 1. Para qué usar Git en sistemas

- Guardar histórico de scripts.
- Documentar cambios de configuración.
- Comparar versiones.
- Trabajar con ramas sin romper la versión estable.
- Revisar cambios antes de aplicarlos.
- Colaborar con otras personas.
- Publicar guías y documentación técnica.

---

## 2. Conceptos básicos

| Concepto | Explicación |
|---|---|
| Repositorio | Carpeta controlada por Git |
| Commit | Punto guardado del historial |
| Rama | Línea de trabajo independiente |
| Remote | Repositorio remoto, como GitHub |
| Clone | Copia local de un repositorio remoto |
| Pull | Descargar cambios remotos |
| Push | Subir cambios locales |
| Merge | Unir cambios de una rama a otra |

---

## 3. Configuración inicial

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --global init.defaultBranch main
git config --list
```

---

## 4. Crear o clonar repositorios

Crear repositorio local:

```bash
git init
```

Clonar repositorio remoto:

```bash
git clone URL_DEL_REPOSITORIO
```

Ver remoto configurado:

```bash
git remote -v
```

---

## 5. Flujo básico

```bash
git status
git add archivo.md
git add .
git commit -m "Describe el cambio"
git push
```

Antes de subir cambios conviene revisar:

```bash
git diff
git status
```

---

## 6. Ramas

```bash
git branch
git branch nueva-rama
git checkout nueva-rama
git checkout -b nueva-rama
git switch main
git switch -c nueva-rama
```

Fusionar cambios:

```bash
git switch main
git merge nueva-rama
```

---

## 7. Historial y diferencias

```bash
git log --oneline
git log --graph --oneline --all
git diff
git diff archivo.md
git show HASH_COMMIT
```

---

## 8. Deshacer cambios

Descartar cambios no guardados en un archivo:

```bash
git checkout -- archivo.md
```

Con Git moderno:

```bash
git restore archivo.md
```

Quitar del área de preparación:

```bash
git restore --staged archivo.md
```

Revertir un commit creando otro commit inverso:

```bash
git revert HASH_COMMIT
```

---

## 9. .gitignore

El archivo `.gitignore` evita subir archivos innecesarios o sensibles.

Ejemplo:

```gitignore
.env
*.log
*.tmp
__pycache__/
node_modules/
*.key
*.pem
backups/
```

Nunca subir:

- Contraseñas.
- Tokens.
- Claves privadas.
- Backups con datos reales.
- Archivos `.env` con credenciales.

---

## 10. GitHub

GitHub permite alojar repositorios y trabajar con:

- Issues.
- Pull requests.
- Wikis.
- Releases.
- Actions.
- GitHub Pages.

Flujo recomendado:

1. Crear rama.
2. Hacer cambios.
3. Commit claro.
4. Push.
5. Pull request.
6. Revisión.
7. Merge.

---

## 11. Buenas prácticas de commits

Un buen commit debe ser pequeño y explicar qué cambia.

Ejemplos:

```text
Añade guía de redes y servicios
Corrige ejemplos de PowerShell
Documenta checklist de backups
```

Evitar mensajes como:

```text
cambios
update
cosas
final final
```

---

## 12. Git aplicado a scripts

Estructura recomendada:

```text
scripts/
├── bash/
├── powershell/
└── python/
```

Cada script debería tener:

- Cabecera con objetivo.
- Ejemplo de uso.
- Parámetros documentados.
- Código probado.
- Sin secretos.

---

## 13. Checklist Git

- [ ] Repositorio inicializado.
- [ ] `.gitignore` creado.
- [ ] No hay secretos en el repo.
- [ ] Commits claros.
- [ ] README actualizado.
- [ ] Ramas usadas para cambios grandes.
- [ ] Pull requests para revisión.
