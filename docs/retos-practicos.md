# Retos prácticos graduados

Estos retos están organizados por dificultad. La idea es practicar autonomía: primero intenta resolverlos sin mirar la solución.

---

## Nivel 1: básico

### Reto 1: carpeta de laboratorio

Crea una carpeta, entra en ella, genera archivos, lista contenido y guarda el resultado.

??? success "Solución orientativa Linux"

    ```bash
    mkdir laboratorio
    cd laboratorio
    touch a.txt b.txt c.txt
    ls -lah > listado.txt
    cat listado.txt
    ```

??? success "Solución orientativa PowerShell"

    ```powershell
    New-Item laboratorio -ItemType Directory
    Set-Location laboratorio
    New-Item a.txt, b.txt, c.txt -ItemType File
    Get-ChildItem > listado.txt
    Get-Content listado.txt
    ```

---

### Reto 2: información del sistema

Obtén nombre del equipo, usuario actual, versión del sistema y fecha.

??? success "Solución orientativa"

    === "Linux"

        ```bash
        hostname
        whoami
        hostnamectl
        date
        ```

    === "PowerShell"

        ```powershell
        hostname
        whoami
        Get-ComputerInfo
        Get-Date
        ```

---

## Nivel 2: administración

### Reto 3: procesos con mayor consumo

Localiza los procesos con mayor consumo de CPU y memoria.

??? success "Solución orientativa Linux"

    ```bash
    ps aux --sort=-%cpu | head
    ps aux --sort=-%mem | head
    ```

??? success "Solución orientativa PowerShell"

    ```powershell
    Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
    Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
    ```

---

### Reto 4: servicios fallidos

Comprueba si hay servicios detenidos o fallidos.

??? success "Solución orientativa"

    === "Linux"

        ```bash
        systemctl --failed
        systemctl list-units --type=service --state=running
        ```

    === "PowerShell"

        ```powershell
        Get-Service | Where-Object {$_.Status -ne "Running"}
        ```

---

## Nivel 3: red

### Reto 5: diagnóstico completo de red

Comprueba IP, ruta, DNS y acceso a un puerto web.

??? success "Solución orientativa"

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

## Nivel 4: scripting

### Reto 6: informe básico Linux

Crea un bloque que guarde en un archivo: fecha, equipo, memoria, disco y servicios fallidos.

??? success "Solución orientativa"

    ```bash
    {
      echo "== Fecha =="
      date
      echo "== Equipo =="
      hostname
      echo "== Memoria =="
      free -h
      echo "== Disco =="
      df -h
      echo "== Servicios fallidos =="
      systemctl --failed || true
    } > informe.txt
    ```

---

### Reto 7: informe básico Windows

Crea un informe con equipo, usuario, disco y servicios detenidos.

??? success "Solución orientativa"

    ```powershell
    $salida = "informe-windows.txt"
    "Equipo: $env:COMPUTERNAME" | Out-File $salida
    "Usuario: $env:USERNAME" | Out-File $salida -Append
    Get-PSDrive | Out-File $salida -Append
    Get-Service | Where-Object {$_.Status -ne "Running"} | Out-File $salida -Append
    ```

---

## Nivel 5: profesional

### Reto 8: runbook de incidencia

Crea un runbook para una incidencia de servicio caído.

Debe incluir:

- Síntomas.
- Impacto.
- Comandos de diagnóstico.
- Pasos de resolución.
- Verificación.
- Rollback.
- Evidencias.

??? success "Estructura orientativa"

    ```text
    Nombre: Servicio no responde
    Síntomas: usuarios no pueden acceder
    Impacto: servicio no disponible
    Diagnóstico: estado, logs, puerto, firewall
    Resolución: corregir causa y reiniciar si procede
    Verificación: servicio activo y puerto accesible
    Rollback: restaurar configuración anterior
    Evidencias: logs y comandos ejecutados
    ```

---

### Reto 9: convertir práctica en proyecto

Elige uno de los retos anteriores y conviértelo en un mini proyecto.

Debe tener:

- README.
- Objetivo.
- Requisitos.
- Comandos.
- Script o pseudocódigo.
- Verificación.
- Mejoras futuras.

---

## Tabla de progreso

| Reto | Tema | Nivel | Completado |
|---|---|---:|---|
| 1 | Archivos | 1 | [ ] |
| 2 | Sistema | 1 | [ ] |
| 3 | Procesos | 2 | [ ] |
| 4 | Servicios | 2 | [ ] |
| 5 | Red | 3 | [ ] |
| 6 | Scripting Linux | 4 | [ ] |
| 7 | Scripting Windows | 4 | [ ] |
| 8 | Runbook | 5 | [ ] |
| 9 | Proyecto | 5 | [ ] |
