# Cheatsheet Redes

Referencia rápida para diagnóstico de red en Linux, Windows CMD y PowerShell.

---

## Configuración IP

| Acción | Linux | CMD | PowerShell |
|---|---|---|---|
| Ver IP | `ip a` | `ipconfig /all` | `Get-NetIPAddress` |
| Ver rutas | `ip route` | `route print` | `Get-NetRoute` |
| Ver DNS | `resolvectl status` | `ipconfig /all` | `Get-DnsClientServerAddress` |

---

## Conectividad

```bash
ping 8.8.8.8
ping google.com
traceroute google.com
```

```cmd
ping 8.8.8.8
ping google.com
tracert google.com
```

```powershell
Test-Connection 8.8.8.8
Test-NetConnection google.com -TraceRoute
```

---

## DNS

```bash
nslookup google.com
dig google.com
dig google.com MX
```

```cmd
nslookup google.com
ipconfig /flushdns
```

```powershell
Resolve-DnsName google.com
Clear-DnsClientCache
```

---

## Puertos

```bash
ss -tulnp
ss -tan
```

```cmd
netstat -ano
netstat -ano | findstr :443
```

```powershell
Get-NetTCPConnection
Test-NetConnection google.com -Port 443
```

---

## HTTP/HTTPS

```bash
curl -I https://example.com
curl -v https://example.com
```

```powershell
Invoke-WebRequest https://example.com
Test-NetConnection example.com -Port 443
```

---

## Puertos comunes

| Servicio | Puerto |
|---|---:|
| SSH | 22 |
| DNS | 53 |
| HTTP | 80 |
| HTTPS | 443 |
| SMB | 445 |
| SMTP | 25 |
| IMAP | 143 |
| IMAPS | 993 |
| RDP | 3389 |
| MySQL/MariaDB | 3306 |
| PostgreSQL | 5432 |

---

## Checklist rápido

- [ ] IP correcta.
- [ ] Máscara correcta.
- [ ] Gateway correcto.
- [ ] DNS correcto.
- [ ] Ping a gateway.
- [ ] Ping a IP externa.
- [ ] Resolución DNS.
- [ ] Puerto abierto.
- [ ] Servicio escuchando.
- [ ] Firewall revisado.
