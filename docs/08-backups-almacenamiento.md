# 08 - Backups y almacenamiento

Un sistema sin copias de seguridad no está administrado de forma segura. Los backups deben ser planificados, automatizados, comprobados y documentados.

---

## 1. Conceptos básicos

| Concepto | Explicación |
|---|---|
| Backup completo | Copia todo el contenido seleccionado |
| Backup incremental | Copia solo cambios desde la última copia |
| Backup diferencial | Copia cambios desde el último backup completo |
| RPO | Cuánta información se puede perder como máximo |
| RTO | Tiempo máximo aceptable para recuperar el servicio |
| Retención | Tiempo que se conservan las copias |
| Restauración | Proceso de recuperar datos desde una copia |

---

## 2. Regla 3-2-1

Una estrategia clásica:

- 3 copias de los datos.
- 2 soportes distintos.
- 1 copia fuera del equipo o fuera de la ubicación principal.

---

## 3. Almacenamiento en Linux

```bash
lsblk
blkid
df -h
du -sh *
mount
findmnt
sudo fdisk -l
```

### Ver uso de disco por directorio

```bash
du -h --max-depth=1 /var | sort -h
```

---

## 4. Almacenamiento en Windows

### CMD

```cmd
wmic logicaldisk get name,size,freespace
```

### PowerShell

```powershell
Get-PSDrive
Get-Volume
Get-Disk
Get-Partition
```

---

## 5. Compresión y empaquetado en Linux

```bash
tar -cvf backup.tar carpeta/
tar -czvf backup.tar.gz carpeta/
tar -xzvf backup.tar.gz
zip -r backup.zip carpeta/
unzip backup.zip
```

---

## 6. Copias con rsync

`rsync` es una herramienta muy potente para sincronizar archivos.

```bash
rsync -avh origen/ destino/
rsync -avh --delete origen/ destino/
rsync -avh origen/ usuario@servidor:/backups/
```

Opciones:

| Opción | Uso |
|---|---|
| `-a` | modo archivo, conserva permisos y estructura |
| `-v` | salida detallada |
| `-h` | tamaños legibles |
| `--delete` | elimina en destino lo que ya no existe en origen |
| `--dry-run` | simula sin copiar realmente |

---

## 7. Copias en Windows con robocopy

```cmd
robocopy C:\Datos D:\Backup /E /Z /R:3 /W:5 /LOG:C:\backup.log
```

Ejemplo espejo:

```cmd
robocopy C:\Datos D:\Backup /MIR /R:3 /W:5 /LOG:C:\backup.log
```

Cuidado: `/MIR` elimina en destino lo que no exista en origen.

---

## 8. Script Bash: backup con fecha

```bash
#!/bin/bash
set -euo pipefail

ORIGEN="/etc"
DESTINO="/backups"
FECHA=$(date +"%Y-%m-%d_%H-%M-%S")
ARCHIVO="$DESTINO/etc_$FECHA.tar.gz"

mkdir -p "$DESTINO"
tar -czf "$ARCHIVO" "$ORIGEN"

echo "Backup creado: $ARCHIVO"
```

---

## 9. Script Bash: backup con retención

```bash
#!/bin/bash
set -euo pipefail

ORIGEN="/etc"
DESTINO="/backups"
RETENCION_DIAS=7
FECHA=$(date +"%Y-%m-%d_%H-%M-%S")

mkdir -p "$DESTINO"
tar -czf "$DESTINO/etc_$FECHA.tar.gz" "$ORIGEN"
find "$DESTINO" -name "etc_*.tar.gz" -mtime +$RETENCION_DIAS -delete
```

---

## 10. Script PowerShell: backup simple

```powershell
$Origen = "C:\Datos"
$Destino = "D:\Backups"
$Fecha = Get-Date -Format "yyyy-MM-dd_HH-mm-ss"
$DestinoFinal = Join-Path $Destino "Datos_$Fecha"

New-Item $DestinoFinal -ItemType Directory -Force
Copy-Item $Origen\* $DestinoFinal -Recurse
Write-Host "Backup creado en $DestinoFinal"
```

---

## 11. Restauración

Un backup no sirve de mucho si nunca se ha probado restaurarlo.

### Linux

```bash
tar -xzvf backup.tar.gz -C /ruta/restauracion
```

### Windows PowerShell

```powershell
Copy-Item D:\Backups\Datos_2025-01-01\* C:\DatosRestaurados -Recurse
```

---

## 12. Checklist de backups

- [ ] ¿Qué datos se copian?
- [ ] ¿Cada cuánto se copian?
- [ ] ¿Dónde se guardan?
- [ ] ¿Cuánto tiempo se conservan?
- [ ] ¿La copia está automatizada?
- [ ] ¿Hay logs?
- [ ] ¿Se comprueba si el backup falla?
- [ ] ¿Se ha probado la restauración?
- [ ] ¿Hay copia fuera del equipo?
- [ ] ¿La copia protege permisos y propietarios?
