# Cheatsheet Git

Referencia rápida de Git para documentación, scripts y administración de sistemas.

---

## Configuración

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --list
```

---

## Crear o clonar

```bash
git init
git clone URL_DEL_REPOSITORIO
```

---

## Flujo básico

```bash
git status
git add archivo.md
git add .
git commit -m "Mensaje claro"
git push
git pull
```

---

## Ramas

```bash
git branch
git checkout -b nueva-rama
git switch main
git switch -c nueva-rama
git merge nueva-rama
```

---

## Historial

```bash
git log --oneline
git log --graph --oneline --all
git diff
git show HASH
```

---

## Deshacer cambios

```bash
git restore archivo.md
git restore --staged archivo.md
git revert HASH
```

---

## Remotos

```bash
git remote -v
git remote add origin URL_DEL_REPOSITORIO
git push -u origin main
```

---

## Buenas prácticas

- Hacer commits pequeños.
- Escribir mensajes claros.
- Revisar `git status` antes de confirmar cambios.
- Revisar `git diff` antes de subir cambios.
- Usar ramas para cambios grandes.
- Mantener actualizado el README.
