# 05 - Redes y servicios

La administración de sistemas depende de entender redes. Muchos problemas de servidores no son del programa en sí, sino de IP, DNS, puertos, firewall, rutas o servicios caídos.

---

## 1. Conceptos esenciales

| Concepto | Explicación |
|---|---|
| IP | Dirección lógica de un equipo en red |
| Máscara | Define qué parte de la IP pertenece a la red |
| Gateway | Puerta de salida hacia otras redes |
| DNS | Traduce nombres a direcciones IP |
| DHCP | Asigna configuración IP automáticamente |
| Puerto | Punto de entrada lógico de un servicio |
| Socket | Combinación IP + puerto + protocolo |
| NAT | Traducción de direcciones entre redes |
| Firewall | Filtra tráfico permitido o bloqueado |

---

## 2. Ver configuración IP

### Linux

```bash
ip a
ip route
resolvectl status
cat /etc/resolv.conf
```

### Windows CMD

```cmd
ipconfig /all
route print
```

### PowerShell

```powershell
Get-NetIPAddress
Get-NetIPConfiguration
Get-NetRoute
Get-DnsClientServerAddress
```

---

## 3. Probar conectividad

### Ping

```bash
ping 8.8.8.8
ping google.com
```

```cmd
ping 8.8.8.8
ping google.com
```

```powershell
Test-Connection 8.8.8.8
Test-Connection google.com
```

### Interpretación

- Si responde una IP pero no un dominio, probablemente hay problema DNS.
- Si no responde ninguna IP externa, revisar gateway, rutas o firewall.
- Si responde localmente pero no fuera, revisar salida a Internet.

---

## 4. Rutas

### Linux

```bash
ip route
ip route get 8.8.8.8
```

### Windows

```cmd
route print
tracert 8.8.8.8
```

### PowerShell

```powershell
Get-NetRoute
Test-NetConnection 8.8.8.8 -TraceRoute
```

---

## 5. DNS

### Linux

```bash
nslookup google.com
dig google.com
dig google.com A
dig google.com MX
```

### Windows CMD

```cmd
nslookup google.com
ipconfig /displaydns
ipconfig /flushdns
```

### PowerShell

```powershell
Resolve-DnsName google.com
Clear-DnsClientCache
Get-DnsClientCache
```

---

## 6. Puertos y conexiones

### Linux

```bash
ss -tulnp
ss -tan
lsof -i :80
```

### Windows CMD

```cmd
netstat -ano
netstat -ano | findstr :80
```

### PowerShell

```powershell
Get-NetTCPConnection
Get-NetTCPConnection -LocalPort 80
Test-NetConnection servidor.com -Port 443
```

---

## 7. Puertos comunes

| Servicio | Puerto | Protocolo |
|---|---:|---|
| SSH | 22 | TCP |
| FTP | 21 | TCP |
| SFTP | 22 | TCP |
| DNS | 53 | TCP/UDP |
| DHCP | 67/68 | UDP |
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| SMB | 445 | TCP |
| SMTP | 25 | TCP |
| IMAP | 143 | TCP |
| IMAPS | 993 | TCP |
| POP3 | 110 | TCP |
| RDP | 3389 | TCP |
| MySQL/MariaDB | 3306 | TCP |
| PostgreSQL | 5432 | TCP |

---

## 8. Diagnóstico HTTP/HTTPS

### Linux

```bash
curl -I https://example.com
curl -v https://example.com
wget https://example.com/archivo.zip
```

### PowerShell

```powershell
Invoke-WebRequest https://example.com
Invoke-RestMethod https://api.github.com
Test-NetConnection example.com -Port 443
```

---

## 9. SSH

### Conexión básica

```bash
ssh usuario@servidor
ssh usuario@192.168.1.10
ssh -p 2222 usuario@servidor
```

### Copiar archivos

```bash
scp archivo.txt usuario@servidor:/ruta/
scp -r carpeta usuario@servidor:/ruta/
rsync -avh origen/ usuario@servidor:/destino/
```

### Claves SSH

```bash
ssh-keygen -t ed25519
ssh-copy-id usuario@servidor
```

---

## 10. Firewall

### Linux con UFW

```bash
sudo ufw status verbose
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw deny 23/tcp
sudo ufw enable
```

### Windows PowerShell

```powershell
Get-NetFirewallProfile
Get-NetFirewallRule
New-NetFirewallRule -DisplayName "Permitir HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

---

## 11. Método de diagnóstico por capas

Cuando algo no conecta, revisar de abajo arriba:

1. ¿Hay enlace físico o adaptador activo?
2. ¿Tiene IP correcta?
3. ¿Tiene máscara correcta?
4. ¿Tiene gateway?
5. ¿Responde el gateway?
6. ¿Hay DNS?
7. ¿El puerto remoto está abierto?
8. ¿El servicio está escuchando?
9. ¿El firewall permite tráfico?
10. ¿La aplicación responde correctamente?

---

## 12. Script Bash: comprobar conectividad básica

```bash
#!/bin/bash
set -euo pipefail

HOST="${1:-8.8.8.8}"

if ping -c 4 "$HOST"; then
    echo "Conectividad correcta con $HOST"
else
    echo "No hay conectividad con $HOST"
    exit 1
fi
```

---

## 13. Script PowerShell: comprobar puerto

```powershell
param(
    [string]$HostDestino = "google.com",
    [int]$Puerto = 443
)

$Resultado = Test-NetConnection $HostDestino -Port $Puerto

if ($Resultado.TcpTestSucceeded) {
    Write-Host "Puerto $Puerto abierto en $HostDestino"
} else {
    Write-Host "Puerto $Puerto cerrado o inaccesible en $HostDestino"
    exit 1
}
```

---

## 14. Script Python: comprobar varios puertos

```python
import socket

objetivos = [
    ("google.com", 80),
    ("google.com", 443),
    ("127.0.0.1", 22),
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

## 15. Checklist de incidencia de red

- [ ] Confirmar IP local.
- [ ] Confirmar máscara.
- [ ] Confirmar gateway.
- [ ] Probar ping al gateway.
- [ ] Probar ping a IP externa.
- [ ] Probar resolución DNS.
- [ ] Probar puerto concreto.
- [ ] Revisar firewall local.
- [ ] Revisar servicio remoto.
- [ ] Revisar logs.
