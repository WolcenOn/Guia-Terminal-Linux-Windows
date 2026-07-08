# Ejemplos por escenario

Esta página muestra qué comandos y documentos usar según el problema o el rol.

---

## Escenario 1: soy estudiante y estoy empezando

### Objetivo

Aprender a moverme por la terminal sin miedo.

### Qué estudiar

1. [Terminal y comandos](01-terminal-y-comandos.md)
2. [Búsqueda rápida de comandos](busqueda-rapida-comandos.md)
3. [Actividades interactivas](actividades-interactivas.md)
4. [Retos prácticos](retos-practicos.md)

### Práctica mínima

```bash
pwd
ls -lah
mkdir practica
cd practica
touch prueba.txt
cat prueba.txt
```

---

## Escenario 2: tengo que revisar un servidor Linux

### Objetivo

Hacer una revisión inicial sin cambiar nada.

### Comandos

```bash
hostnamectl
uptime
free -h
df -h
ps aux --sort=-%cpu | head
systemctl --failed
journalctl -p err -n 50 --no-pager
ip a
ip route
ss -tulnp
```

### Documentos relacionados

- [Linux administración](03-linux-administracion.md)
- [Procesos, servicios y logs](07-procesos-servicios-logs.md)
- [Monitorización](16-monitorizacion.md)
- [Proyecto final](proyecto-final-web.md)

---

## Escenario 3: tengo que revisar un equipo Windows

### Objetivo

Obtener estado general con PowerShell.

### Comandos

```powershell
Get-ComputerInfo
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-PSDrive
Get-NetIPAddress
Get-Service | Where-Object {$_.Status -ne "Running"}
Get-EventLog -LogName System -EntryType Error -Newest 20
```

### Documentos relacionados

- [Windows CMD y PowerShell](04-windows-cmd-powershell.md)
- [Búsqueda rápida](busqueda-rapida-comandos.md)
- [Casos prácticos](casos-practicos.md)

---

## Escenario 4: la red falla

### Objetivo

Separar problema de IP, gateway, DNS, puerto o servicio.

### Orden recomendado

1. Ver IP.
2. Ver ruta.
3. Probar IP externa.
4. Probar DNS.
5. Probar puerto.
6. Revisar firewall.

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

---

## Escenario 5: quiero crear un script útil

### Objetivo

Pasar de comandos manuales a automatización.

### Proceso

```text
Comando manual -> bloque de comandos -> script con variables -> script con parámetros -> script con logs -> herramienta documentada
```

### Documentos relacionados

- [Fundamentos de scripting](02-fundamentos-scripting.md)
- [Automatización profesional](12-automatizacion-profesional.md)
- [Integración con Script-Lab](19-integracion-script-lab.md)

---

## Escenario 6: quiero preparar una práctica evaluable

### Entregables recomendados

- Objetivo de la práctica.
- Comandos usados.
- Salidas relevantes.
- Explicación del diagnóstico.
- Script si aplica.
- Checklist completado.
- Conclusiones.

### Documentos relacionados

- [Guía docente](guia-docente.md)
- [Retos prácticos](retos-practicos.md)
- [Proyecto final](proyecto-final-web.md)

---

## Escenario 7: quiero avanzar hacia nivel profesional

### Ruta

1. [Git y GitHub](14-git-github.md)
2. [Docker y contenedores](15-docker-contenedores.md)
3. [Monitorización](16-monitorizacion.md)
4. [Runbooks e incidencias](17-runbooks-incidencias.md)
5. [Ansible e IaC](18-ansible-iac.md)
6. [Proyecto final](proyecto-final-web.md)

### Meta

Ser capaz de documentar, automatizar, verificar y mantener procedimientos técnicos.
