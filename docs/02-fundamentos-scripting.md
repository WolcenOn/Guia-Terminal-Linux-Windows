# 02 - Fundamentos de scripting

Un script es un conjunto de instrucciones guardadas en un archivo para ejecutar tareas de forma repetible. En administración de sistemas, los scripts se usan para automatizar mantenimiento, despliegues, inventarios, backups, auditorías, monitorización y resolución de incidencias.

---

## 1. Qué problema resuelve un script

Un script es útil cuando una tarea cumple una o varias condiciones:

- Se repite muchas veces.
- Tiene pasos claros.
- Debe ejecutarse igual en varios equipos.
- Necesita generar un informe.
- Requiere comprobar estados del sistema.
- Puede producir errores si se hace manualmente.
- Forma parte de un procedimiento de mantenimiento.

Ejemplos:

- Crear usuarios automáticamente.
- Comprobar espacio en disco.
- Reiniciar un servicio si está caído.
- Hacer copia de seguridad de una carpeta.
- Leer logs y buscar errores.
- Comprobar puertos abiertos.
- Generar inventario de hardware y software.

---

## 2. Lenguajes principales

| Lenguaje | Mejor para | Sistemas |
|---|---|---|
| Bash | Automatización rápida, servidores Linux, mantenimiento | Linux/Unix |
| PowerShell | Administración de Windows, servicios, usuarios, eventos, objetos | Windows/Linux/macOS con PowerShell Core |
| Python | Automatización multiplataforma, APIs, logs, informes, herramientas avanzadas | Multiplataforma |

---

## 3. Estructura mental de un script

Antes de escribir código, conviene responder:

1. ¿Qué quiero conseguir?
2. ¿Qué datos necesito?
3. ¿Qué comandos o funciones voy a usar?
4. ¿Qué puede salir mal?
5. ¿Cómo sabré si ha funcionado?
6. ¿Dónde guardaré logs o resultados?
7. ¿Se puede ejecutar sin romper nada?

---

## 4. Plantilla lógica universal

Casi cualquier script serio puede organizarse así:

```text
1. Configuración
2. Validación de requisitos
3. Entrada de datos o parámetros
4. Funciones auxiliares
5. Ejecución principal
6. Gestión de errores
7. Registro de logs
8. Salida o informe
9. Código de retorno
```

---

## 5. Variables

Las variables guardan valores reutilizables.

### Bash

```bash
SERVICIO="ssh"
RUTA_BACKUP="/backups"
echo "Servicio: $SERVICIO"
```

### PowerShell

```powershell
$Servicio = "Spooler"
$RutaBackup = "C:\Backups"
Write-Host "Servicio: $Servicio"
```

### Python

```python
servicio = "ssh"
ruta_backup = "/backups"
print(f"Servicio: {servicio}")
```

---

## 6. Condicionales

Permiten tomar decisiones.

### Bash

```bash
if systemctl is-active --quiet ssh; then
    echo "SSH está activo"
else
    echo "SSH está detenido"
fi
```

### PowerShell

```powershell
$Servicio = Get-Service -Name Spooler

if ($Servicio.Status -eq "Running") {
    Write-Host "Spooler está activo"
} else {
    Write-Host "Spooler está detenido"
}
```

### Python

```python
import subprocess

resultado = subprocess.run(["systemctl", "is-active", "ssh"], capture_output=True, text=True)

if resultado.stdout.strip() == "active":
    print("SSH está activo")
else:
    print("SSH está detenido")
```

---

## 7. Bucles

Permiten repetir acciones.

### Bash

```bash
for servicio in ssh cron nginx; do
    systemctl status "$servicio" --no-pager
done
```

### PowerShell

```powershell
$Servicios = @("Spooler", "WinRM", "wuauserv")

foreach ($Servicio in $Servicios) {
    Get-Service -Name $Servicio
}
```

### Python

```python
servicios = ["ssh", "cron", "nginx"]

for servicio in servicios:
    print(f"Comprobando {servicio}")
```

---

## 8. Funciones

Una función agrupa lógica reutilizable.

### Bash

```bash
comprobar_servicio() {
    local servicio="$1"

    if systemctl is-active --quiet "$servicio"; then
        echo "$servicio activo"
    else
        echo "$servicio detenido"
    fi
}

comprobar_servicio ssh
```

### PowerShell

```powershell
function Comprobar-Servicio {
    param([string]$Nombre)

    $Servicio = Get-Service -Name $Nombre -ErrorAction SilentlyContinue

    if ($Servicio) {
        Write-Host "$Nombre está $($Servicio.Status)"
    } else {
        Write-Host "$Nombre no existe"
    }
}

Comprobar-Servicio -Nombre "Spooler"
```

### Python

```python
def comprobar_servicio(nombre):
    print(f"Comprobando {nombre}")

comprobar_servicio("ssh")
```

---

## 9. Parámetros

Los parámetros hacen que un script sea reutilizable.

### Bash

```bash
#!/bin/bash

SERVICIO="$1"

echo "Comprobando servicio: $SERVICIO"
```

Uso:

```bash
./comprobar.sh ssh
```

### PowerShell

```powershell
param(
    [string]$Servicio
)

Write-Host "Comprobando servicio: $Servicio"
```

Uso:

```powershell
.\comprobar.ps1 -Servicio Spooler
```

### Python

```python
import argparse

parser = argparse.ArgumentParser(description="Comprobar un servicio")
parser.add_argument("servicio", help="Nombre del servicio")
args = parser.parse_args()

print(f"Comprobando servicio: {args.servicio}")
```

Uso:

```bash
python comprobar.py ssh
```

---

## 10. Gestión de errores

Un script profesional debe fallar de forma controlada.

### Bash

```bash
#!/bin/bash
set -euo pipefail

cp /origen/archivo /destino/archivo
```

- `-e`: termina si un comando falla.
- `-u`: error si se usa una variable no definida.
- `pipefail`: detecta errores en tuberías.

### PowerShell

```powershell
try {
    Copy-Item "C:\origen\archivo.txt" "C:\destino\archivo.txt" -ErrorAction Stop
}
catch {
    Write-Host "Error: $_"
    exit 1
}
```

### Python

```python
from pathlib import Path

try:
    contenido = Path("archivo.txt").read_text(encoding="utf-8")
except FileNotFoundError:
    print("El archivo no existe")
except Exception as error:
    print(f"Error inesperado: {error}")
```

---

## 11. Logs

Los logs permiten saber qué hizo el script y cuándo.

### Bash

```bash
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

log "Inicio del script"
```

### PowerShell

```powershell
function Write-Log {
    param([string]$Mensaje)
    Write-Host "[$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')] $Mensaje"
}

Write-Log "Inicio del script"
```

### Python

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s"
)

logging.info("Inicio del script")
```

---

## 12. Modo dry-run

Un modo `dry-run` simula lo que haría el script sin aplicar cambios. Es muy útil en tareas peligrosas.

Ejemplo lógico:

```text
Si dry-run está activado:
    mostrar qué se haría
Si no:
    ejecutar cambios reales
```

### Bash simple

```bash
DRY_RUN=true

if [ "$DRY_RUN" = true ]; then
    echo "Simulación: se eliminaría archivo.log"
else
    rm archivo.log
fi
```

---

## 13. Plantilla base Bash

```bash
#!/bin/bash
set -euo pipefail

LOG_FILE="./script.log"
DRY_RUN=false

log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

main() {
    log "Inicio"

    # Código principal aquí

    log "Fin"
}

main "$@"
```

---

## 14. Plantilla base PowerShell

```powershell
param(
    [switch]$DryRun
)

function Write-Log {
    param([string]$Mensaje)
    Write-Host "[$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')] $Mensaje"
}

try {
    Write-Log "Inicio"

    if ($DryRun) {
        Write-Log "Modo simulación activado"
    }

    # Código principal aquí

    Write-Log "Fin"
}
catch {
    Write-Log "Error: $_"
    exit 1
}
```

---

## 15. Plantilla base Python

```python
#!/usr/bin/env python3

import argparse
import logging
from pathlib import Path

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s"
)

def main():
    parser = argparse.ArgumentParser(description="Plantilla base de script")
    parser.add_argument("--dry-run", action="store_true", help="Simula sin aplicar cambios")
    parser.add_argument("--ruta", default=".", help="Ruta de trabajo")
    args = parser.parse_args()

    ruta = Path(args.ruta)

    logging.info("Inicio")
    logging.info(f"Ruta: {ruta}")

    if args.dry_run:
        logging.info("Modo simulación activado")

    # Código principal aquí

    logging.info("Fin")

if __name__ == "__main__":
    main()
```

---

## 16. Cómo pasar de comando a script

Ejemplo: comprobar espacio en disco.

### Comando manual

```bash
df -h
```

### Comando filtrado

```bash
df -h | grep /dev/
```

### Script básico

```bash
#!/bin/bash

df -h | grep /dev/
```

### Script más útil

```bash
#!/bin/bash
set -euo pipefail

UMBRAL=80

df -h | awk 'NR>1 {print $5 " " $6}' | while read uso particion; do
    porcentaje=${uso%\%}

    if [ "$porcentaje" -ge "$UMBRAL" ]; then
        echo "ALERTA: $particion está al $uso"
    fi
done
```

---

## 17. Errores comunes

- Crear scripts sin objetivo claro.
- No validar parámetros.
- No controlar errores.
- Usar rutas absolutas incorrectas.
- No usar comillas en variables con espacios.
- Ejecutar como administrador/root sin necesidad.
- No dejar logs.
- No probar en entorno seguro.
- Mezclar configuración y lógica.
- No documentar qué hace el script.

---

## 18. Checklist para crear un script

Antes de dar un script por terminado:

- [ ] Tiene un objetivo claro.
- [ ] Tiene nombre descriptivo.
- [ ] Incluye comentarios donde aportan valor.
- [ ] Valida entradas.
- [ ] Controla errores.
- [ ] Tiene logs.
- [ ] Puede probarse sin causar daño.
- [ ] Usa rutas y permisos adecuados.
- [ ] Devuelve salida comprensible.
- [ ] Está documentado en el repositorio.
