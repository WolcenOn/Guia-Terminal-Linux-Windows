# Ejercicios resueltos

Soluciones orientativas para comparar después de intentarlo.

!!! warning "Importante"

    Intenta resolver cada ejercicio antes de abrir la solución.

---

## 1. Terminal básica

=== "Linux"

    ```bash
    mkdir laboratorio
    cd laboratorio
    touch uno.txt dos.txt tres.txt
    ls -lah > listado.txt
    grep "uno" listado.txt
    ```

=== "PowerShell"

    ```powershell
    New-Item laboratorio -ItemType Directory
    Set-Location laboratorio
    New-Item uno.txt, dos.txt, tres.txt -ItemType File
    Get-ChildItem > listado.txt
    Select-String "uno" listado.txt
    ```

---

## 2. Diagnóstico Linux

```bash
hostnamectl
uptime
free -h
df -h
ps aux --sort=-%cpu | head
systemctl --failed
```

---

## 3. Inventario PowerShell

```powershell
$Inventario = [PSCustomObject]@{
    Equipo = $env:COMPUTERNAME
    Usuario = $env:USERNAME
    Sistema = (Get-CimInstance Win32_OperatingSystem).Caption
    Fecha = Get-Date
}

$Inventario | Format-List
```

---

## 4. Diagnóstico de red

=== "Linux"

    ```bash
    ip a
    ip route
    ping -c 4 8.8.8.8
    nslookup example.com
    curl -I https://example.com
    ```

=== "PowerShell"

    ```powershell
    Get-NetIPAddress
    Get-NetRoute
    Test-Connection 8.8.8.8
    Resolve-DnsName example.com
    Test-NetConnection example.com -Port 443
    ```

---

## 5. Backup simple

1. Crear datos de prueba.
2. Crear una copia.
3. Verificar que existe.
4. Restaurar en una carpeta distinta.
5. Documentar resultado.

---

## 6. Git básico

```bash
git init
echo "# Repo de prueba" > README.md
git add README.md
git commit -m "Añade README inicial"
git switch -c mejora-readme
```

---

## 7. Informe de mantenimiento

```bash
{
    echo "== Fecha =="
    date
    echo "== Equipo =="
    hostname
    echo "== Disco =="
    df -h
    echo "== Memoria =="
    free -h
} > mantenimiento.txt
```

---

## Siguiente paso

Realiza los laboratorios completos en [Script-Lab](../script-lab.md).
