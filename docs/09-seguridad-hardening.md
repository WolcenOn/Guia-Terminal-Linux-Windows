# 09 - Seguridad y hardening

La seguridad en administración de sistemas consiste en reducir riesgos, limitar privilegios, mantener sistemas actualizados, controlar accesos, revisar logs y tener capacidad de recuperación.

---

## 1. Principios básicos

- Mínimo privilegio.
- Defensa en profundidad.
- Actualizaciones frecuentes.
- Copias de seguridad verificadas.
- Servicios expuestos solo si son necesarios.
- Contraseñas y claves protegidas.
- Logs revisables.
- Documentación de cambios.

---

## 2. Revisión inicial Linux

```bash
hostnamectl
who
w
last
id
sudo -l
ss -tulnp
systemctl --failed
journalctl -p err -n 50
sudo ufw status verbose
```

---

## 3. Revisión inicial Windows

```powershell
Get-ComputerInfo
Get-LocalUser
Get-LocalGroupMember Administrators
Get-NetFirewallProfile
Get-Service
Get-EventLog -LogName System -EntryType Error -Newest 20
Get-MpComputerStatus
```

---

## 4. Actualizaciones

### Debian/Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt autoremove
```

### Red Hat/Fedora/Rocky/Alma

```bash
sudo dnf update
```

### Windows PowerShell

Windows Update suele gestionarse con herramientas del sistema, WSUS, Intune o módulos específicos. Como comprobación básica:

```powershell
Get-HotFix | Sort-Object InstalledOn -Descending | Select-Object -First 10
```

---

## 5. SSH seguro

Archivo habitual:

```bash
/etc/ssh/sshd_config
```

Recomendaciones comunes:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Aplicar cambios:

```bash
sudo sshd -t
sudo systemctl restart ssh
```

Antes de cerrar la sesión actual, abrir otra sesión SSH para verificar que el acceso sigue funcionando.

---

## 6. Firewall

### UFW

```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw status numbered
```

### Windows

```powershell
Get-NetFirewallProfile
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled True
Get-NetFirewallRule | Where-Object {$_.Enabled -eq "True"}
```

---

## 7. Servicios expuestos

### Linux

```bash
ss -tulnp
systemctl list-units --type=service --state=running
```

### Windows

```powershell
Get-NetTCPConnection | Where-Object {$_.State -eq "Listen"}
Get-Service | Where-Object {$_.Status -eq "Running"}
```

Si un servicio no se usa, deshabilitarlo reduce superficie de ataque.

---

## 8. Permisos peligrosos

### Linux

Buscar archivos con permisos demasiado abiertos:

```bash
find /ruta -type f -perm 777
find /ruta -type d -perm 777
```

Buscar binarios SUID:

```bash
find / -perm -4000 -type f 2>/dev/null
```

### Windows

```cmd
icacls C:\Datos
```

Revisar especialmente carpetas compartidas, scripts, backups y datos sensibles.

---

## 9. Gestión de secretos

Malas prácticas:

- Contraseñas dentro de scripts.
- Tokens en repositorios públicos.
- Archivos `.env` subidos a GitHub.
- Claves privadas sin protección.

Buenas prácticas:

- Usar variables de entorno.
- Usar gestores de secretos.
- Añadir `.env` y claves privadas a `.gitignore`.
- Rotar credenciales si han sido expuestas.

---

## 10. Auditoría básica

### Linux

```bash
last
lastlog
sudo grep "Failed password" /var/log/auth.log
sudo grep "sudo" /var/log/auth.log
```

### Windows

```powershell
Get-WinEvent -LogName Security -MaxEvents 100
Get-LocalGroupMember Administrators
```

---

## 11. Script Bash: revisión rápida de seguridad

```bash
#!/bin/bash
set -euo pipefail

echo "== Usuarios conectados =="
who

echo "== Servicios escuchando =="
ss -tulnp

echo "== Servicios fallidos =="
systemctl --failed || true

echo "== Errores recientes =="
journalctl -p err -n 20 --no-pager || true
```

---

## 12. Checklist de hardening inicial

- [ ] Sistema actualizado.
- [ ] Firewall activo.
- [ ] Solo puertos necesarios abiertos.
- [ ] SSH sin login directo de root.
- [ ] Usuarios antiguos eliminados o deshabilitados.
- [ ] Administradores revisados.
- [ ] Permisos sensibles comprobados.
- [ ] Backups funcionando.
- [ ] Logs disponibles.
- [ ] Servicios innecesarios deshabilitados.
- [ ] Secretos fuera del repositorio.
