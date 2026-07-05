# Plantillas de scripts

Este archivo recopila plantillas iniciales para scripts de administración. En esta guía se documentan como referencia; las versiones completas y ejecutables pueden trasladarse después a Script-Lab.

---

## 1. Inventario de sistema en Bash

```bash
#!/bin/bash
set -euo pipefail

echo "== Inventario del sistema =="
echo "Fecha: $(date)"
echo "Equipo: $(hostname)"
echo "Usuario: $(whoami)"

echo "== Sistema =="
uname -a

echo "== Memoria =="
free -h

echo "== Disco =="
df -h

echo "== Red =="
ip a
```

---

## 2. Comprobación de servicios en Bash

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

## 3. Inventario en PowerShell

```powershell
$Inventario = [PSCustomObject]@{
    Equipo = $env:COMPUTERNAME
    Usuario = $env:USERNAME
    Sistema = (Get-CimInstance Win32_OperatingSystem).Caption
    CPU = (Get-CimInstance Win32_Processor).Name
    RAM_GB = [math]::Round((Get-CimInstance Win32_ComputerSystem).TotalPhysicalMemory / 1GB, 2)
    Fecha = Get-Date
}

$Inventario | Format-List
```

---

## 4. Comprobación de puerto en PowerShell

```powershell
param(
    [string]$HostDestino = "example.com",
    [int]$Puerto = 443
)

$Resultado = Test-NetConnection $HostDestino -Port $Puerto

if ($Resultado.TcpTestSucceeded) {
    Write-Host "Puerto abierto"
} else {
    Write-Host "Puerto cerrado o inaccesible"
    exit 1
}
```

---

## 5. Comprobación de puertos en Python

```python
import socket

objetivos = [
    ("example.com", 80),
    ("example.com", 443),
]

def comprobar(host, puerto, timeout=2):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        return s.connect_ex((host, puerto)) == 0

for host, puerto in objetivos:
    estado = "abierto" if comprobar(host, puerto) else "cerrado"
    print(f"{host}:{puerto} {estado}")
```

---

## 6. Plantilla profesional mínima

Todo script serio debería incorporar:

- Objetivo claro.
- Parámetros.
- Validación de entrada.
- Control de errores.
- Logs.
- Salida comprensible.
- Documentación.
- Modo de prueba si modifica datos.

---

## 7. Cuándo pasar una plantilla a Script-Lab

Una plantilla puede moverse a Script-Lab cuando:

- Está probada.
- Tiene README o comentario de uso.
- No contiene credenciales.
- Funciona en un entorno de prueba.
- Tiene ejemplo de ejecución.
- Tiene gestión de errores.
