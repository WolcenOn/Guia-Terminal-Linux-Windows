# Ejercicios resueltos

Estos ejercicios resueltos sirven como referencia inicial. No sustituyen la práctica: lo ideal es intentar resolverlos primero y luego comparar.

---

## 1. Terminal básica

### Enunciado

Crear una carpeta de laboratorio, crear archivos, listar contenido, guardar salida y limpiar el entorno.

### Linux

```bash
mkdir laboratorio
cd laboratorio
touch uno.txt dos.txt tres.txt
ls -lah > listado.txt
grep "uno" listado.txt
rm uno.txt dos.txt tres.txt listado.txt
cd ..
rmdir laboratorio
```

### PowerShell

```powershell
New-Item laboratorio -ItemType Directory
Set-Location laboratorio
New-Item uno.txt, dos.txt, tres.txt -ItemType File
Get-ChildItem > listado.txt
Select-String "uno" listado.txt
Remove-Item uno.txt, dos.txt, tres.txt, listado.txt
Set-Location ..
Remove-Item laboratorio
```

---

## 2. Diagnóstico básico Linux

### Enunciado

Obtener información del sistema y guardarla en un archivo.

### Solución

```bash
{
    echo "== Sistema =="
    hostnamectl
    echo
    echo "== Memoria =="
    free -h
    echo
    echo "== Disco =="
    df -h
    echo
    echo "== Procesos CPU =="
    ps aux --sort=-%cpu | head
    echo
    echo "== Servicios fallidos =="
    systemctl --failed || true
} > informe-linux.txt
```

### Verificación

```bash
cat informe-linux.txt
```

---

## 3. Inventario PowerShell

### Enunciado

Crear inventario básico y exportarlo a CSV.

### Solución

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

$Inventario | Export-Csv .\inventario.csv -NoTypeInformation
$Inventario | Format-List
```

### Verificación

```powershell
Get-Content .\inventario.csv
```

---

## 4. Diagnóstico de red

### Enunciado

Comprobar IP, gateway, DNS y puerto remoto.

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

### Interpretación

- Si la IP externa responde pero el dominio no resuelve, revisar DNS.
- Si no responde la IP externa, revisar gateway o salida de red.
- Si el puerto falla, revisar servicio, firewall o destino.

---

## 5. Backup simple Linux

### Enunciado

Crear una copia comprimida con fecha.

### Solución

```bash
mkdir -p origen backups
echo "dato de prueba" > origen/dato.txt
FECHA=$(date +"%Y-%m-%d_%H-%M-%S")
tar -czf "backups/origen_$FECHA.tar.gz" origen/
ls -lah backups/
```

### Restauración de prueba

```bash
mkdir restaurado
tar -xzf backups/origen_*.tar.gz -C restaurado
find restaurado -type f
```

---

## 6. Git básico

### Enunciado

Crear un repositorio local, hacer commit y trabajar con una rama.

### Solución

```bash
mkdir repo-prueba
cd repo-prueba
git init
echo "# Repo de prueba" > README.md
git add README.md
git commit -m "Añade README inicial"
git switch -c mejora-readme
echo "Contenido adicional" >> README.md
git diff
git add README.md
git commit -m "Amplía README"
git switch main
git merge mejora-readme
```

---

## 7. Informe de mantenimiento básico

### Enunciado

Generar una revisión rápida de sistema Linux.

### Solución

```bash
{
    echo "== Fecha =="
    date
    echo "== Equipo =="
    hostname
    echo "== Uptime =="
    uptime
    echo "== Disco =="
    df -h
    echo "== Memoria =="
    free -h
    echo "== Servicios fallidos =="
    systemctl --failed || true
    echo "== Errores recientes =="
    journalctl -p err -n 20 --no-pager || true
} > mantenimiento.txt
```

---

## 8. Revisión de servicios PowerShell

### Enunciado

Listar servicios automáticos que no estén en ejecución.

### Solución

```powershell
Get-Service | Where-Object {
    $_.StartType -eq "Automatic" -and $_.Status -ne "Running"
} | Select-Object Name, Status, StartType
```

---

## 9. Comprobación de puertos con Python

### Enunciado

Comprobar si varios puertos están abiertos.

### Solución

```python
import socket

objetivos = [
    ("example.com", 80),
    ("example.com", 443),
]

for host, puerto in objetivos:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(2)
        abierto = s.connect_ex((host, puerto)) == 0
        estado = "abierto" if abierto else "cerrado"
        print(f"{host}:{puerto} {estado}")
```

---

## 10. Conclusión

Estos ejercicios forman una primera base práctica. El siguiente paso es convertirlos en scripts parametrizables, con logs, control de errores y documentación para Script-Lab.
