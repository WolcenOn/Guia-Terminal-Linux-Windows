# Checklist de mantenimiento de sistemas

Checklist práctico para revisar sistemas Linux y Windows de forma periódica.

---

## 1. Estado general

- [ ] El sistema arranca correctamente.
- [ ] La hora y zona horaria son correctas.
- [ ] El nombre del equipo está documentado.
- [ ] La versión del sistema operativo está identificada.
- [ ] No hay reinicios inesperados.

### Linux

```bash
hostnamectl
uptime
timedatectl
```

### Windows

```powershell
Get-ComputerInfo
Get-Date
systeminfo
```

---

## 2. Recursos

- [ ] CPU sin uso sostenido anormal.
- [ ] Memoria suficiente.
- [ ] Disco con espacio libre.
- [ ] No hay particiones críticas llenas.
- [ ] No hay procesos bloqueados o anómalos.

### Linux

```bash
uptime
free -h
df -h
ps aux --sort=-%cpu | head
```

### Windows

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-PSDrive
```

---

## 3. Servicios

- [ ] Servicios críticos activos.
- [ ] Servicios fallidos revisados.
- [ ] Servicios innecesarios deshabilitados.
- [ ] Puertos expuestos documentados.

### Linux

```bash
systemctl --failed
systemctl list-units --type=service --state=running
ss -tulnp
```

### Windows

```powershell
Get-Service
Get-NetTCPConnection | Where-Object {$_.State -eq "Listen"}
```

---

## 4. Logs

- [ ] Logs de sistema revisados.
- [ ] Errores recientes identificados.
- [ ] Logs de aplicaciones críticas revisados.
- [ ] Logs no llenan el disco.

### Linux

```bash
journalctl -p err -n 50
ls -lh /var/log
```

### Windows

```powershell
Get-EventLog -LogName System -EntryType Error -Newest 20
Get-EventLog -LogName Application -EntryType Error -Newest 20
```

---

## 5. Red

- [ ] IP correcta.
- [ ] Gateway correcto.
- [ ] DNS correcto.
- [ ] Servicios accesibles.
- [ ] Firewall revisado.

### Linux

```bash
ip a
ip route
ping -c 4 8.8.8.8
ss -tulnp
```

### Windows

```powershell
Get-NetIPAddress
Get-NetRoute
Test-Connection 8.8.8.8
Get-NetFirewallProfile
```

---

## 6. Usuarios y permisos

- [ ] Usuarios antiguos revisados.
- [ ] Administradores revisados.
- [ ] Permisos sensibles comprobados.
- [ ] No hay cuentas compartidas sin justificar.
- [ ] Accesos recientes revisados.

### Linux

```bash
getent passwd
getent group
last
```

### Windows

```powershell
Get-LocalUser
Get-LocalGroupMember Administrators
```

---

## 7. Backups

- [ ] Backup reciente existente.
- [ ] Backup sin errores.
- [ ] Espacio en destino suficiente.
- [ ] Retención aplicada.
- [ ] Restauración probada periódicamente.

---

## 8. Seguridad

- [ ] Sistema actualizado.
- [ ] Firewall activo.
- [ ] Servicios expuestos justificados.
- [ ] Credenciales protegidas.
- [ ] Claves privadas fuera de repositorios.
- [ ] Logs de autenticación revisados.

---

## 9. Documentación

- [ ] Cambios recientes documentados.
- [ ] Scripts actualizados.
- [ ] Runbooks actualizados.
- [ ] Inventario actualizado.
- [ ] Incidencias cerradas con evidencias.
