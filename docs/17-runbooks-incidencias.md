# 17 - Runbooks e incidencias

Un runbook es un procedimiento documentado para actuar ante una tarea repetitiva o una incidencia. En administración profesional no basta con saber comandos: hay que saber en qué orden usarlos, qué comprobar y cómo documentar el resultado.

---

## 1. Qué debe tener un runbook

- Nombre del procedimiento.
- Objetivo.
- Síntomas o caso de uso.
- Impacto posible.
- Requisitos previos.
- Pasos de diagnóstico.
- Pasos de resolución.
- Verificación.
- Rollback o vuelta atrás.
- Evidencias que guardar.
- Responsable o equipo.

---

## 2. Plantilla base

```text
Nombre:
Objetivo:
Sistema afectado:
Síntomas:
Impacto:
Requisitos:
Diagnóstico:
Resolución:
Verificación:
Rollback:
Evidencias:
Notas:
```

---

## 3. Runbook: disco lleno en Linux

### Síntomas

- Aplicación deja de escribir.
- Logs con errores de espacio.
- Servicios fallan.
- `df -h` muestra una partición al 90% o más.

### Diagnóstico

```bash
df -h
du -h --max-depth=1 /var | sort -h
journalctl -p err -n 50
```

### Resolución segura

1. Identificar la partición afectada.
2. Localizar directorios que más ocupan.
3. Revisar logs, cachés o backups antiguos.
4. No borrar datos sin saber su función.
5. Mover o rotar archivos si procede.
6. Verificar espacio liberado.

### Verificación

```bash
df -h
systemctl --failed
```

---

## 4. Runbook: servicio caído en Linux

### Diagnóstico

```bash
systemctl status servicio
journalctl -u servicio -n 50 --no-pager
ss -tulnp
```

### Resolución

```bash
sudo systemctl restart servicio
systemctl status servicio
```

### Verificación

- Servicio activo.
- Puerto escuchando si aplica.
- Logs sin errores nuevos.
- Aplicación responde.

---

## 5. Runbook: problemas DNS

### Diagnóstico

```bash
ping 8.8.8.8
ping example.com
nslookup example.com
cat /etc/resolv.conf
```

PowerShell:

```powershell
Test-Connection 8.8.8.8
Resolve-DnsName example.com
Get-DnsClientServerAddress
```

### Interpretación

- Si responde IP pero no dominio, revisar DNS.
- Si no responde IP, revisar gateway o conectividad.
- Si resuelve mal, revisar servidor DNS configurado.

---

## 6. Runbook: puerto no accesible

### Diagnóstico

Linux:

```bash
ss -tulnp
curl -I http://localhost
sudo ufw status
```

PowerShell:

```powershell
Test-NetConnection destino -Port 443
Get-NetTCPConnection
Get-NetFirewallProfile
```

### Posibles causas

- Servicio apagado.
- Servicio escuchando en otra IP o puerto.
- Firewall local bloqueando.
- Firewall externo bloqueando.
- DNS apuntando a otro servidor.

---

## 7. Runbook: backup fallido

### Diagnóstico

- Revisar log del backup.
- Comprobar espacio en destino.
- Comprobar permisos.
- Comprobar conectividad si es remoto.
- Comprobar si el origen existe.

Comandos útiles:

```bash
df -h
ls -lah /backups
journalctl -p err -n 50
```

PowerShell:

```powershell
Get-PSDrive
Get-ChildItem D:\Backups
Get-EventLog -LogName System -EntryType Error -Newest 20
```

---

## 8. Runbook: usuario sin acceso

### Linux

```bash
id usuario
groups usuario
sudo passwd -S usuario
last usuario
```

### Windows

```powershell
Get-LocalUser usuario
Get-LocalGroupMember Administrators
```

### Revisar

- Usuario existe.
- Cuenta no bloqueada.
- Contraseña correcta.
- Grupo adecuado.
- Permisos sobre el recurso.
- Logs de autenticación.

---

## 9. Evidencias

En una incidencia conviene guardar:

- Fecha y hora.
- Comandos ejecutados.
- Salidas relevantes.
- Logs afectados.
- Cambios realizados.
- Resultado final.
- Medidas preventivas.

---

## 10. Checklist de cierre de incidencia

- [ ] Causa identificada.
- [ ] Servicio restaurado.
- [ ] Verificación realizada.
- [ ] Logs revisados.
- [ ] Cambios documentados.
- [ ] Riesgos comunicados si aplica.
- [ ] Prevención propuesta.
- [ ] Runbook actualizado.
