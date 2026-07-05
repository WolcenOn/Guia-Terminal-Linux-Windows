# Cheatsheet PowerShell

Referencia rápida de PowerShell para administración de sistemas Windows.

---

## Ayuda

```powershell
Get-Help Comando
Get-Help Comando -Examples
Get-Command *Service*
Get-Member
```

## Sistema

```powershell
Get-ComputerInfo
Get-Date
hostname
whoami
$env:USERNAME
$env:COMPUTERNAME
```

## Archivos

```powershell
Get-Location
Set-Location C:\Ruta
Get-ChildItem
New-Item archivo.txt -ItemType File
New-Item carpeta -ItemType Directory
Copy-Item origen destino
Move-Item origen destino
Remove-Item archivo
Get-Content archivo
Select-String "texto" archivo
```

## Procesos

```powershell
Get-Process
Get-Process -Name notepad
Stop-Process -Id 1234
Stop-Process -Name notepad -Force
```

## Servicios

```powershell
Get-Service
Get-Service -Name Spooler
Start-Service Spooler
Stop-Service Spooler
Restart-Service Spooler
Set-Service Spooler -StartupType Automatic
```

## Usuarios y grupos

```powershell
Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember Administrators
New-LocalUser "usuario" -Password (Read-Host -AsSecureString)
Add-LocalGroupMember -Group "Administrators" -Member "usuario"
```

## Red

```powershell
Get-NetIPAddress
Get-NetAdapter
Get-NetRoute
Test-Connection 8.8.8.8
Test-NetConnection google.com -Port 443
Resolve-DnsName google.com
Get-NetTCPConnection
```

## Eventos

```powershell
Get-EventLog -LogName System -Newest 20
Get-EventLog -LogName Application -EntryType Error -Newest 20
Get-WinEvent -LogName System -MaxEvents 50
```

## Firewall

```powershell
Get-NetFirewallProfile
Get-NetFirewallRule
New-NetFirewallRule -DisplayName "Permitir HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

## Exportar datos

```powershell
Get-Process | Export-Csv procesos.csv -NoTypeInformation
Get-Service | ConvertTo-Json
```
