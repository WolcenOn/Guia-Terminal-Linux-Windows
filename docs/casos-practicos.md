# Casos prácticos guiados

Los casos prácticos están pensados para aprender a diagnosticar. Cada caso plantea una situación realista, propone pasos de análisis y muestra una solución orientativa.

---

## Caso 1: el disco está casi lleno

!!! failure "Situación"

    Un servidor empieza a mostrar errores al escribir logs. La aplicación responde lentamente y algunos servicios fallan.

### Objetivo

Detectar qué partición está llena y localizar los directorios que más ocupan.

### Diagnóstico Linux

```bash
df -h
du -h --max-depth=1 /var | sort -h
journalctl -p err -n 50 --no-pager
```

### Diagnóstico Windows

```powershell
Get-PSDrive
Get-Volume
Get-ChildItem C:\ -Directory | Select-Object FullName
```

### Preguntas

??? question "¿Qué mirarías primero?"

    Primero revisaría el uso de disco por unidad o partición. Después localizaría carpetas grandes y comprobaría logs, temporales o backups acumulados.

??? question "¿Qué no deberías hacer?"

    No deberías borrar carpetas del sistema sin saber qué contienen. Primero hay que identificar, documentar y actuar sobre elementos seguros.

### Cierre

- Documentar qué ocupaba espacio.
- Indicar cuánto espacio se liberó.
- Proponer rotación de logs o política de retención.

---

## Caso 2: no hay conexión a Internet

!!! failure "Situación"

    Un equipo no navega. El usuario dice que “Internet no funciona”.

### Diagnóstico por capas

1. IP local.
2. Gateway.
3. Salida a IP externa.
4. DNS.
5. Puerto o servicio.

### Linux

```bash
ip a
ip route
ping -c 4 8.8.8.8
nslookup example.com
curl -I https://example.com
```

### PowerShell

```powershell
Get-NetIPAddress
Get-NetRoute
Test-Connection 8.8.8.8
Resolve-DnsName example.com
Test-NetConnection example.com -Port 443
```

??? question "Si responde 8.8.8.8 pero no resuelve dominios, ¿dónde está el problema?"

    Probablemente en DNS.

??? question "Si no responde ni siquiera la IP externa, ¿qué revisarías?"

    IP local, máscara, gateway, rutas, firewall y conectividad física o virtual.

---

## Caso 3: un servicio no responde

!!! failure "Situación"

    Un servicio aparece instalado, pero los usuarios no pueden acceder.

### Linux

```bash
systemctl status servicio
journalctl -u servicio -n 50 --no-pager
ss -tulnp
sudo ufw status
```

### PowerShell

```powershell
Get-Service servicio
Get-EventLog -LogName System -EntryType Error -Newest 20
Get-NetTCPConnection
Test-NetConnection localhost -Port 80
```

### Posibles causas

- Servicio detenido.
- Servicio con error de configuración.
- Puerto incorrecto.
- Firewall bloqueando.
- Servicio escuchando solo en localhost.
- Dependencia caída.

??? success "Resolución orientativa"

    1. Confirmar estado del servicio.
    2. Revisar logs.
    3. Confirmar puerto.
    4. Probar acceso local.
    5. Probar acceso remoto.
    6. Revisar firewall.
    7. Reiniciar solo si procede y documentarlo.

---

## Caso 4: un usuario no puede acceder

!!! failure "Situación"

    Un usuario indica que no puede iniciar sesión o no puede acceder a una carpeta.

### Linux

```bash
id usuario
groups usuario
getent passwd usuario
last usuario
ls -ld /ruta/recurso
```

### Windows

```powershell
Get-LocalUser usuario
Get-LocalGroupMember Administrators
Get-Acl C:\Ruta\Recurso
```

### Revisar

- La cuenta existe.
- La cuenta está habilitada.
- Pertenece al grupo correcto.
- La contraseña no está bloqueada o caducada.
- El recurso tiene permisos correctos.
- Hay errores de autenticación en logs.

---

## Caso 5: un backup ha fallado

!!! failure "Situación"

    La tarea de backup no ha generado copia o la copia pesa menos de lo esperado.

### Diagnóstico

```bash
df -h
ls -lah /backups
journalctl -p err -n 50 --no-pager
```

```powershell
Get-PSDrive
Get-ChildItem D:\Backups
Get-EventLog -LogName System -EntryType Error -Newest 20
```

### Preguntas clave

- ¿Hay espacio suficiente?
- ¿Existe la carpeta origen?
- ¿Existe el destino?
- ¿Hay permisos?
- ¿Se puede restaurar?
- ¿La tarea estaba programada?

??? warning "Punto importante"

    Un backup que no se ha probado restaurando no debe considerarse fiable.

---

## Caso 6: demasiados procesos consumen CPU

!!! failure "Situación"

    El equipo va lento y el ventilador trabaja constantemente.

### Linux

```bash
uptime
top
ps aux --sort=-%cpu | head
```

### PowerShell

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
```

### Decisión

Antes de terminar procesos:

- Identificar qué proceso es.
- Comprobar si es crítico.
- Revisar desde cuándo consume.
- Ver si hay logs asociados.
- Documentar la acción.

---

## Caso 7: preparar informe de mantenimiento

!!! example "Reto final"

    Genera un informe que incluya sistema, red, disco, memoria, servicios, logs y recomendaciones.

### Entregables

- Informe Markdown o TXT.
- Comandos utilizados.
- Capturas o salidas relevantes.
- Diagnóstico final.
- Acciones recomendadas.

[Ver proyecto final](proyecto-final-web.md)
