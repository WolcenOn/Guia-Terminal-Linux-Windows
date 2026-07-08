# Búsqueda rápida de comandos

Esta página funciona como índice práctico: busca por tarea, no por nombre de comando. Es útil cuando sabes lo que quieres hacer, pero no recuerdas el comando exacto.

!!! tip "Cómo usar esta página"

    Usa el buscador de la web o `Ctrl + F` y escribe palabras como: `disco`, `usuario`, `servicio`, `puerto`, `DNS`, `backup`, `proceso`, `logs`, `permisos`.

---

## Sistema

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver nombre del equipo | `hostname` | `hostname` | `$env:COMPUTERNAME` |
| Ver usuario actual | `whoami` | `whoami` | `$env:USERNAME` |
| Ver información del sistema | `hostnamectl` | `systeminfo` | `Get-ComputerInfo` |
| Ver tiempo encendido | `uptime` | `systeminfo` | `(Get-CimInstance Win32_OperatingSystem).LastBootUpTime` |
| Ver fecha y hora | `date` | `date /t` | `Get-Date` |

??? example "Ejemplo: informe rápido del equipo"

    === "Linux"

        ```bash
        hostnamectl
        uptime
        whoami
        ```

    === "PowerShell"

        ```powershell
        Get-ComputerInfo
        Get-Date
        whoami
        ```

---

## Archivos y carpetas

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver ubicación actual | `pwd` | `cd` | `Get-Location` |
| Listar archivos | `ls -lah` | `dir` | `Get-ChildItem` |
| Crear carpeta | `mkdir carpeta` | `mkdir carpeta` | `New-Item carpeta -ItemType Directory` |
| Copiar archivo | `cp origen destino` | `copy origen destino` | `Copy-Item origen destino` |
| Mover archivo | `mv origen destino` | `move origen destino` | `Move-Item origen destino` |
| Eliminar archivo | `rm archivo` | `del archivo` | `Remove-Item archivo` |
| Ver archivo | `cat archivo` | `type archivo` | `Get-Content archivo` |
| Buscar texto | `grep "texto" archivo` | `findstr "texto" archivo` | `Select-String "texto" archivo` |

!!! warning "Cuidado"

    Antes de borrar, comprueba siempre la ruta y el contenido. En laboratorios usa carpetas de prueba.

---

## Disco y almacenamiento

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver discos y particiones | `lsblk` | `wmic logicaldisk get name,size,freespace` | `Get-Volume` |
| Ver espacio libre | `df -h` | `dir` | `Get-PSDrive` |
| Ver tamaño de carpeta | `du -sh carpeta` | `dir /s` | `(Get-ChildItem carpeta -Recurse | Measure-Object Length -Sum).Sum` |
| Ver UUID/dispositivos | `blkid` | `mountvol` | `Get-Volume` |

??? example "Ejemplo: detectar particiones llenas en Linux"

    ```bash
    df -h
    du -h --max-depth=1 /var | sort -h
    ```

---

## Procesos

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver procesos | `ps aux` | `tasklist` | `Get-Process` |
| Ordenar por CPU | `ps aux --sort=-%cpu` | `tasklist` | `Get-Process | Sort-Object CPU -Descending` |
| Buscar proceso | `pgrep nombre` | `tasklist | findstr nombre` | `Get-Process nombre` |
| Terminar proceso | `kill PID` | `taskkill /PID PID` | `Stop-Process -Id PID` |

---

## Servicios

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver servicios | `systemctl list-units --type=service` | `sc query` | `Get-Service` |
| Ver estado | `systemctl status servicio` | `sc query servicio` | `Get-Service servicio` |
| Iniciar | `systemctl start servicio` | `net start servicio` | `Start-Service servicio` |
| Detener | `systemctl stop servicio` | `net stop servicio` | `Stop-Service servicio` |
| Reiniciar | `systemctl restart servicio` | `sc stop servicio` + `sc start servicio` | `Restart-Service servicio` |
| Ver fallidos | `systemctl --failed` | `sc query state= inactive` | `Get-Service | Where-Object {$_.Status -ne "Running"}` |

---

## Logs y eventos

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver errores recientes | `journalctl -p err -n 50` | `wevtutil qe System /c:20` | `Get-EventLog -LogName System -EntryType Error -Newest 20` |
| Ver logs de un servicio | `journalctl -u servicio -n 50` | `wevtutil` | `Get-WinEvent` |
| Seguir un log | `tail -f archivo.log` | — | `Get-Content archivo.log -Wait` |

---

## Red

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver IP | `ip a` | `ipconfig /all` | `Get-NetIPAddress` |
| Ver ruta | `ip route` | `route print` | `Get-NetRoute` |
| Probar conectividad | `ping 8.8.8.8` | `ping 8.8.8.8` | `Test-Connection 8.8.8.8` |
| Resolver DNS | `nslookup dominio` | `nslookup dominio` | `Resolve-DnsName dominio` |
| Ver puertos | `ss -tulnp` | `netstat -ano` | `Get-NetTCPConnection` |
| Probar puerto | `nc -vz host puerto` | — | `Test-NetConnection host -Port puerto` |

??? question "Caso rápido: IP responde pero dominio no"

    Si puedes hacer ping a una IP externa pero no resolver un dominio, probablemente el problema está en DNS.

---

## Usuarios y permisos

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Ver usuario actual | `id` | `whoami` | `whoami` |
| Ver usuarios | `getent passwd` | `net user` | `Get-LocalUser` |
| Ver grupos | `getent group` | `net localgroup` | `Get-LocalGroup` |
| Cambiar permisos | `chmod` | `icacls` | `Get-Acl` / `Set-Acl` |
| Cambiar propietario | `chown` | `takeown` | `Set-Acl` |

---

## Backups

| Quiero... | Linux | Windows CMD | PowerShell |
|---|---|---|---|
| Comprimir carpeta | `tar -czf copia.tar.gz carpeta` | — | `Compress-Archive carpeta copia.zip` |
| Sincronizar carpetas | `rsync -av origen/ destino/` | `robocopy origen destino /E` | `Copy-Item origen destino -Recurse` |
| Verificar copia | `tar -tzf copia.tar.gz` | `dir destino` | `Get-ChildItem destino` |

---

## Git y Docker

| Quiero... | Git | Docker |
|---|---|---|
| Ver estado | `git status` | `docker ps` |
| Guardar cambios | `git add . && git commit -m "mensaje"` | — |
| Subir cambios | `git push` | — |
| Ver imágenes | — | `docker images` |
| Ejecutar contenedor | — | `docker run imagen` |
| Ver logs | — | `docker logs contenedor` |

---

## Siguiente paso

- Para aprender el contexto, vuelve al tema correspondiente.
- Para practicar, usa [Casos prácticos](casos-practicos.md).
- Para autoevaluarte, usa [Actividades interactivas](actividades-interactivas.md).
