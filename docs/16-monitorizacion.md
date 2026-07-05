# 16 - Monitorización y observabilidad

Monitorizar consiste en comprobar el estado de sistemas y servicios para detectar problemas antes de que afecten a los usuarios. Observar un sistema no es solo mirar si está encendido: hay que revisar métricas, logs, eventos, disponibilidad y tendencias.

---

## 1. Qué se debe monitorizar

| Área | Ejemplos |
|---|---|
| CPU | Uso medio, carga, procesos con mayor consumo |
| Memoria | RAM usada, swap, presión de memoria |
| Disco | Espacio libre, uso por partición, I/O |
| Red | Latencia, pérdida, puertos, conexiones |
| Servicios | Estado activo, reinicios, errores |
| Logs | Errores, autenticación, eventos críticos |
| Seguridad | Accesos fallidos, cambios de permisos, usuarios |
| Backups | Última copia, tamaño, resultado, restauración |

---

## 2. Comandos rápidos Linux

```bash
uptime
free -h
df -h
du -sh /var/*
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
systemctl --failed
journalctl -p err -n 50
ss -tulnp
```

---

## 3. Comandos rápidos Windows PowerShell

```powershell
Get-ComputerInfo
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
Get-Service | Where-Object {$_.Status -ne "Running"}
Get-EventLog -LogName System -EntryType Error -Newest 20
Get-PSDrive
Get-NetTCPConnection
```

---

## 4. Métricas frente a logs

| Tipo | Uso |
|---|---|
| Métricas | Valores numéricos: CPU, RAM, disco, latencia |
| Logs | Eventos detallados: errores, accesos, cambios |
| Trazas | Seguimiento de una petición o proceso completo |
| Alertas | Avisos cuando una condición supera un umbral |

---

## 5. Umbrales orientativos

Estos valores dependen del entorno, pero sirven como punto de partida:

| Recurso | Aviso | Crítico |
|---|---:|---:|
| Disco | 80% | 90% |
| CPU sostenida | 75% | 90% |
| Memoria | 80% | 95% |
| Swap | uso constante | crecimiento continuo |
| Errores de servicio | repetidos | servicio caído |

---

## 6. Monitorización de servicios

### Linux

```bash
systemctl is-active ssh
systemctl is-enabled ssh
journalctl -u ssh -n 50
```

### PowerShell

```powershell
Get-Service -Name Spooler
Get-Service | Where-Object {$_.StartType -eq "Automatic" -and $_.Status -ne "Running"}
```

---

## 7. Monitorización de disco

### Linux

```bash
df -h
df -h | awk 'NR>1 {print $5, $6}'
```

### PowerShell

```powershell
Get-PSDrive -PSProvider FileSystem
Get-Volume
```

---

## 8. Monitorización de red

```bash
ping -c 4 8.8.8.8
ss -tulnp
curl -I https://example.com
```

```powershell
Test-Connection 8.8.8.8
Test-NetConnection example.com -Port 443
```

---

## 9. Alertas

Una alerta debe tener:

- Qué ha fallado.
- Dónde ha fallado.
- Cuándo ha fallado.
- Nivel de gravedad.
- Impacto posible.
- Acción recomendada.

Ejemplo:

```text
CRITICO: servidor-db01 tiene /var al 92%. Revisar logs y liberar espacio o ampliar volumen.
```

---

## 10. Herramientas profesionales

| Herramienta | Uso habitual |
|---|---|
| Prometheus | Recolección de métricas |
| Grafana | Paneles visuales |
| Zabbix | Monitorización completa de infraestructura |
| Nagios/Icinga | Monitorización de servicios y hosts |
| Elastic / OpenSearch | Centralización y búsqueda de logs |
| Loki | Logs integrados con Grafana |
| Netdata | Monitorización rápida de sistemas |

---

## 11. Script conceptual: informe rápido Linux

```bash
#!/bin/bash
set -euo pipefail

echo "== Estado general =="
uptime

echo "== Memoria =="
free -h

echo "== Disco =="
df -h

echo "== Servicios fallidos =="
systemctl --failed || true

echo "== Errores recientes =="
journalctl -p err -n 20 --no-pager || true
```

---

## 12. Checklist de monitorización

- [ ] CPU controlada.
- [ ] Memoria controlada.
- [ ] Disco controlado.
- [ ] Servicios críticos monitorizados.
- [ ] Puertos críticos revisados.
- [ ] Logs de error revisados.
- [ ] Backups monitorizados.
- [ ] Alertas definidas.
- [ ] Umbrales documentados.
- [ ] Procedimiento de respuesta definido.
