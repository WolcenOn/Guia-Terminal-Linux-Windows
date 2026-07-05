# Proyecto final - Informe de mantenimiento de sistemas

Este proyecto integra varios bloques de la guía: terminal, administración Linux/Windows, redes, servicios, logs, backups, seguridad, scripting, documentación y procedimientos.

---

## 1. Objetivo

Crear un procedimiento completo para revisar el estado de un sistema y generar un informe de mantenimiento.

El proyecto debe poder evolucionar en tres fases:

1. Ejecución manual con comandos.
2. Script semiautomatizado.
3. Herramienta completa en Script-Lab.

---

## 2. Alcance

El informe debe revisar:

- Información general del sistema.
- CPU, memoria y disco.
- Red y conectividad.
- Servicios críticos.
- Procesos con mayor consumo.
- Logs o eventos recientes.
- Usuarios y permisos relevantes.
- Estado de backups.
- Recomendaciones finales.

---

## 3. Requisitos

### Linux

- Bash.
- Permisos suficientes para consultar servicios y logs.
- Herramientas básicas: `df`, `free`, `ps`, `systemctl`, `journalctl`, `ip`, `ss`.

### Windows

- PowerShell.
- Permisos suficientes para consultar servicios y eventos.
- Cmdlets básicos de sistema, red y eventos.

---

## 4. Estructura del informe

```text
Informe de mantenimiento
├── Fecha y equipo
├── Sistema operativo
├── Recursos
│   ├── CPU
│   ├── Memoria
│   └── Disco
├── Red
├── Servicios
├── Procesos
├── Logs o eventos
├── Usuarios y permisos
├── Backups
└── Conclusiones
```

---

## 5. Fase 1: comandos manuales Linux

```bash
hostnamectl
uptime
free -h
df -h
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
ip a
ip route
ss -tulnp
systemctl --failed
journalctl -p err -n 50 --no-pager
last | head
```

---

## 6. Fase 1: comandos manuales Windows

```powershell
Get-ComputerInfo
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
Get-PSDrive
Get-NetIPAddress
Get-NetRoute
Get-Service | Where-Object {$_.Status -ne "Running"}
Get-EventLog -LogName System -EntryType Error -Newest 20
Get-LocalUser
Get-LocalGroupMember Administrators
```

---

## 7. Fase 2: informe Linux en bloque

```bash
{
    echo "# Informe de mantenimiento Linux"
    echo
    echo "## Fecha"
    date
    echo
    echo "## Sistema"
    hostnamectl
    echo
    echo "## Uptime"
    uptime
    echo
    echo "## Memoria"
    free -h
    echo
    echo "## Disco"
    df -h
    echo
    echo "## Procesos por CPU"
    ps aux --sort=-%cpu | head
    echo
    echo "## Red"
    ip a
    ip route
    echo
    echo "## Puertos escuchando"
    ss -tulnp
    echo
    echo "## Servicios fallidos"
    systemctl --failed || true
    echo
    echo "## Errores recientes"
    journalctl -p err -n 50 --no-pager || true
} > informe-mantenimiento-linux.md
```

---

## 8. Fase 2: informe Windows en bloque

```powershell
$Informe = "informe-mantenimiento-windows.txt"

"# Informe de mantenimiento Windows" | Out-File $Informe
"Fecha: $(Get-Date)" | Out-File $Informe -Append
"Equipo: $env:COMPUTERNAME" | Out-File $Informe -Append
"Usuario: $env:USERNAME" | Out-File $Informe -Append

"`n## Sistema" | Out-File $Informe -Append
Get-ComputerInfo | Out-File $Informe -Append

"`n## Procesos por CPU" | Out-File $Informe -Append
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 | Out-File $Informe -Append

"`n## Disco" | Out-File $Informe -Append
Get-PSDrive | Out-File $Informe -Append

"`n## Red" | Out-File $Informe -Append
Get-NetIPAddress | Out-File $Informe -Append

"`n## Servicios detenidos" | Out-File $Informe -Append
Get-Service | Where-Object {$_.Status -ne "Running"} | Out-File $Informe -Append

"`n## Eventos de error" | Out-File $Informe -Append
Get-EventLog -LogName System -EntryType Error -Newest 20 | Out-File $Informe -Append
```

---

## 9. Fase 3: mejoras profesionales

El script final debería añadir:

- Parámetros.
- Ruta de salida configurable.
- Logs de ejecución.
- Control de errores.
- Modo resumido y modo detallado.
- Exportación a Markdown, TXT, CSV o JSON.
- Umbrales configurables.
- Código de salida.
- Documentación.
- Pruebas.

---

## 10. Parámetros recomendados

```text
--salida informe.md
--formato markdown
--umbral-disco 80
--servicios ssh,nginx,mysql
--incluir-logs
--dry-run
```

---

## 11. Criterios de evaluación

| Criterio | Nivel básico | Nivel avanzado |
|---|---|---|
| Información del sistema | Muestra datos básicos | Genera informe estructurado |
| Recursos | Muestra CPU/RAM/disco | Detecta umbrales |
| Servicios | Lista servicios | Valida servicios críticos |
| Logs | Muestra errores | Clasifica y resume errores |
| Red | Muestra IP | Comprueba conectividad |
| Seguridad | Lista usuarios | Revisa administradores y accesos |
| Automatización | Comandos manuales | Script parametrizable |
| Documentación | Notas básicas | README completo |

---

## 12. Entregables

- Informe generado.
- Comandos utilizados.
- Script o bloque automatizado.
- Explicación de resultados.
- Problemas encontrados.
- Recomendaciones.
- Mejoras futuras.

---

## 13. Evolución hacia Script-Lab

Cuando el proyecto esté probado, se puede dividir en varios scripts:

- `inventario_sistema`.
- `comprobar_disco`.
- `comprobar_servicios`.
- `revisar_logs`.
- `diagnostico_red`.
- `generar_informe_mantenimiento`.

Cada script debe tener documentación propia y ejemplos de uso.
