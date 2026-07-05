# 04 - Windows: CMD y PowerShell

Windows se puede administrar desde interfaces gráficas, pero CMD y PowerShell permiten diagnosticar, automatizar y repetir tareas de forma profesional.

---

## 1. CMD frente a PowerShell

| Herramienta | Enfoque | Uso recomendado |
|---|---|---|
| CMD | Comandos clásicos basados en texto | Diagnóstico rápido, comandos heredados, compatibilidad |
| PowerShell | Shell orientado a objetos | Administración moderna, scripting, automatización avanzada |

PowerShell trabaja con objetos. Esto permite filtrar, ordenar y exportar información de forma mucho más potente que CMD.

---

## 2. Información del sistema

### CMD

```cmd
hostname
whoami
ver
systeminfo
wmic os get caption,version,osarchitecture
```

### PowerShell

```powershell
hostname
whoami
Get-ComputerInfo
Get-CimInstance Win32_OperatingSystem
Get-CimInstance Win32_ComputerSystem
Get-CimInstance Win32_Processor
```

---

## 3. Archivos y carpetas

### CMD

```cmd
dir
cd C:\Ruta
mkdir carpeta
rmdir carpeta
copy origen destino
xcopy origen destino /E /I
robocopy origen destino /MIR
move origen destino
del archivo.txt
type archivo.txt
```

### PowerShell

```powershell
Get-ChildItem
Set-Location C:\Ruta
New-Item carpeta -ItemType Directory
Remove-Item carpeta -Recurse
Copy-Item origen destino
Move-Item origen destino
Get-Content archivo.txt
Select-String "error" archivo.log
```

### Robocopy

`robocopy` es una herramienta muy útil para copias robustas en Windows.

```cmd
robocopy C:\Origen D:\Backup /E /Z /R:3 /W:5 /LOG:backup.log
```

- `/E`: copia subdirectorios, incluidos vacíos.
- `/Z`: modo reiniciable.
- `/R:3`: tres reintentos.
- `/W:5`: espera cinco segundos entre reintentos.
- `/LOG`: guarda log.

---

## 4. Procesos

### CMD

```cmd
tasklist
tasklist | findstr chrome
taskkill /PID 1234
taskkill /IM notepad.exe /F
```

### PowerShell

```powershell
Get-Process
Get-Process -Name notepad
Stop-Process -Name notepad
Stop-Process -Id 1234 -Force
```

---

## 5. Servicios

### CMD

```cmd
sc query
sc query Spooler
net start Spooler
net stop Spooler
sc start Spooler
sc stop Spooler
```

### PowerShell

```powershell
Get-Service
Get-Service -Name Spooler
Start-Service Spooler
Stop-Service Spooler
Restart-Service Spooler
Set-Service Spooler -StartupType Automatic
```

---

## 6. Usuarios y grupos locales

### CMD

```cmd
net user
net user usuario contraseña /add
net user usuario /delete
net localgroup
net localgroup administrators usuario /add
```

### PowerShell

```powershell
Get-LocalUser
New-LocalUser "usuario" -Password (Read-Host -AsSecureString)
Remove-LocalUser "usuario"
Get-LocalGroup
Add-LocalGroupMember -Group "Administrators" -Member "usuario"
Get-LocalGroupMember Administrators
```

---

## 7. Red en Windows

### CMD

```cmd
ipconfig /all
ping 8.8.8.8
tracert google.com
nslookup google.com
netstat -ano
route print
arp -a
```

### PowerShell

```powershell
Get-NetIPAddress
Get-NetAdapter
Get-NetRoute
Test-Connection 8.8.8.8
Test-NetConnection google.com -Port 443
Resolve-DnsName google.com
Get-NetTCPConnection
```

---

## 8. Firewall de Windows

```powershell
Get-NetFirewallProfile
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled True
Get-NetFirewallRule | Where-Object {$_.Enabled -eq "True"}
New-NetFirewallRule -DisplayName "Permitir HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

---

## 9. Eventos y logs

### Visor de eventos desde PowerShell

```powershell
Get-EventLog -LogName System -Newest 20
Get-EventLog -LogName Application -EntryType Error -Newest 20
Get-WinEvent -LogName System -MaxEvents 50
```

### Buscar errores

```powershell
Get-WinEvent -LogName System -MaxEvents 100 | Where-Object {$_.LevelDisplayName -eq "Error"}
```

---

## 10. Tareas programadas

```powershell
Get-ScheduledTask

$Accion = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File C:\Scripts\mantenimiento.ps1"
$Trigger = New-ScheduledTaskTrigger -Daily -At 02:00
Register-ScheduledTask -TaskName "MantenimientoDiario" -Action $Accion -Trigger $Trigger
```

---

## 11. Inventario básico con PowerShell

```powershell
$Inventario = [PSCustomObject]@{
    Equipo = $env:COMPUTERNAME
    Usuario = $env:USERNAME
    Sistema = (Get-CimInstance Win32_OperatingSystem).Caption
    Version = (Get-CimInstance Win32_OperatingSystem).Version
    CPU = (Get-CimInstance Win32_Processor).Name
    RAM_GB = [math]::Round((Get-CimInstance Win32_ComputerSystem).TotalPhysicalMemory / 1GB, 2)
    Fecha = Get-Date
}

$Inventario | Format-List
$Inventario | Export-Csv ".\inventario.csv" -NoTypeInformation
```

---

## 12. Buenas prácticas

- Ejecutar PowerShell como administrador solo cuando haga falta.
- Usar `Get-Help` antes de comandos nuevos.
- Evitar cambiar políticas de ejecución sin entender el impacto.
- Guardar logs en scripts de mantenimiento.
- Preferir PowerShell para automatización compleja.
- Usar `-WhatIf` cuando esté disponible para simular cambios.

---

## 13. Checklist de diagnóstico rápido

```powershell
Get-ComputerInfo
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Service | Where-Object {$_.Status -eq "Stopped"}
Get-EventLog -LogName System -EntryType Error -Newest 20
Get-NetIPAddress
Test-NetConnection google.com -Port 443
Get-PSDrive
```
