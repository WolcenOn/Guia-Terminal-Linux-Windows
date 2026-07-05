# 07 - Procesos, servicios y logs

Cuando un sistema falla, normalmente hay que revisar tres cosas: qué procesos están ejecutándose, qué servicios están activos y qué dicen los logs.

---

## 1. Procesos

Un proceso es un programa en ejecución. Cada proceso tiene un identificador llamado PID.

### Linux

```bash
ps aux
top
htop
pgrep nginx
pidof sshd
kill PID
kill -15 PID
kill -9 PID
```

### Windows CMD

```cmd
tasklist
taskkill /PID 1234
taskkill /IM notepad.exe /F
```

### PowerShell

```powershell
Get-Process
Get-Process -Name notepad
Stop-Process -Id 1234
Stop-Process -Name notepad -Force
```

---

## 2. Interpretar consumo

| Métrica | Qué indica |
|---|---|
| CPU | Uso de procesador |
| RAM | Memoria usada |
| PID | Identificador de proceso |
| Usuario | Cuenta que ejecuta el proceso |
| Tiempo | Tiempo de ejecución o consumo acumulado |

### Linux

```bash
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
```

### PowerShell

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
```

---

## 3. Servicios

Un servicio es un programa que se ejecuta en segundo plano para ofrecer una función: web, base de datos, SSH, impresión, DNS, etc.

### Linux systemd

```bash
systemctl status nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl enable nginx
sudo systemctl disable nginx
systemctl --failed
```

### Windows PowerShell

```powershell
Get-Service
Get-Service -Name Spooler
Start-Service Spooler
Stop-Service Spooler
Restart-Service Spooler
Set-Service Spooler -StartupType Automatic
```

---

## 4. Logs en Linux

### journalctl

```bash
journalctl
journalctl -xe
journalctl -p err
journalctl -u ssh
journalctl -u nginx -f
journalctl --since "1 hour ago"
```

### Archivos habituales

| Archivo | Uso |
|---|---|
| `/var/log/syslog` | Log general en Debian/Ubuntu |
| `/var/log/auth.log` | Autenticación en Debian/Ubuntu |
| `/var/log/messages` | Log general en algunas distribuciones |
| `/var/log/secure` | Seguridad/autenticación en RHEL-like |
| `/var/log/nginx/` | Logs de Nginx |
| `/var/log/apache2/` | Logs de Apache en Debian/Ubuntu |

```bash
tail -f /var/log/syslog
grep -i "error" /var/log/syslog
```

---

## 5. Logs en Windows

### PowerShell

```powershell
Get-EventLog -LogName System -Newest 50
Get-EventLog -LogName Application -EntryType Error -Newest 20
Get-WinEvent -LogName System -MaxEvents 50
```

### Eventos de error

```powershell
Get-WinEvent -LogName System -MaxEvents 100 | Where-Object {$_.LevelDisplayName -eq "Error"}
```

---

## 6. Método de resolución de incidencias

1. Identificar el servicio afectado.
2. Comprobar si está activo.
3. Revisar consumo de CPU/RAM/disco.
4. Leer logs recientes.
5. Revisar cambios recientes.
6. Reiniciar solo si se entiende el impacto.
7. Verificar que el servicio vuelve a responder.
8. Documentar causa, solución y prevención.

---

## 7. Ejemplo: servicio web no responde

### Linux

```bash
systemctl status nginx
journalctl -u nginx -n 50 --no-pager
ss -tulnp | grep :80
curl -I http://localhost
sudo nginx -t
sudo systemctl restart nginx
```

### Windows IIS

```powershell
Get-Service W3SVC
Get-WinEvent -LogName System -MaxEvents 50
Test-NetConnection localhost -Port 80
Restart-Service W3SVC
```

---

## 8. Script Bash: revisar servicios críticos

```bash
#!/bin/bash
set -euo pipefail

SERVICIOS=(ssh cron nginx)

for servicio in "${SERVICIOS[@]}"; do
    if systemctl is-active --quiet "$servicio"; then
        echo "OK: $servicio activo"
    else
        echo "ERROR: $servicio detenido"
    fi
done
```

---

## 9. Script PowerShell: servicios detenidos automáticos

```powershell
Get-Service | Where-Object {
    $_.StartType -eq "Automatic" -and $_.Status -ne "Running"
} | Select-Object Name, Status, StartType
```

---

## 10. Checklist de revisión

- [ ] ¿El proceso existe?
- [ ] ¿Consume CPU o memoria de forma anormal?
- [ ] ¿El servicio está activo?
- [ ] ¿El servicio está habilitado al arranque?
- [ ] ¿El puerto está escuchando?
- [ ] ¿Los logs muestran errores?
- [ ] ¿Hubo cambios recientes?
- [ ] ¿La solución ha sido verificada?
