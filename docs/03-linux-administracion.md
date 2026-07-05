# 03 - Linux: administración del sistema

Este documento reúne los comandos y procedimientos básicos para administrar sistemas Linux desde terminal. La idea no es memorizar comandos aislados, sino entender qué tarea resuelve cada grupo de comandos.

---

## 1. Identificación del sistema

Antes de tocar un sistema conviene saber dónde estamos trabajando.

```bash
hostname
hostnamectl
uname -a
cat /etc/os-release
lsb_release -a
uptime
whoami
id
```

### Uso práctico

- Confirmar distribución y versión antes de instalar paquetes.
- Saber si el sistema usa `systemd`.
- Ver usuario actual y permisos.
- Documentar una incidencia.

---

## 2. Estructura de directorios Linux

| Ruta | Uso habitual |
|---|---|
| `/` | Raíz del sistema |
| `/home` | Directorios de usuarios |
| `/root` | Directorio del administrador root |
| `/etc` | Configuración del sistema |
| `/var` | Datos variables: logs, cachés, colas |
| `/var/log` | Archivos de log |
| `/tmp` | Archivos temporales |
| `/usr` | Programas y librerías de usuario |
| `/bin` y `/sbin` | Binarios esenciales |
| `/opt` | Software adicional |
| `/mnt` y `/media` | Montajes temporales o externos |
| `/dev` | Dispositivos |
| `/proc` | Información del kernel y procesos |

---

## 3. Archivos y directorios

```bash
pwd
ls -lah
cd /ruta
mkdir carpeta
mkdir -p ruta/anidada
rmdir carpeta_vacia
touch archivo.txt
cp origen destino
cp -r carpeta destino
mv origen destino
rm archivo
rm -r carpeta
```

### Buenas prácticas

- Usar `rm -i` si hay riesgo de borrar por error.
- Comprobar rutas con `pwd` antes de eliminar.
- Evitar `rm -rf /ruta` sin revisar exactamente la variable o ruta.

---

## 4. Ver y buscar contenido

```bash
cat archivo.txt
less archivo.txt
head archivo.txt
tail archivo.txt
tail -f /var/log/syslog
grep "error" archivo.log
grep -R "texto" /etc
find /var/log -name "*.log"
```

### Ejemplo útil

Buscar errores recientes en logs:

```bash
grep -Ri "error" /var/log | tail -n 50
```

---

## 5. Permisos y propietarios

```bash
ls -l
chmod 755 script.sh
chmod +x script.sh
chmod -R 750 carpeta
chown usuario:grupo archivo
chown -R usuario:grupo carpeta
umask
```

### Lectura de permisos

Ejemplo:

```text
-rwxr-xr--
```

- Primer carácter: tipo de archivo.
- `rwx`: permisos del propietario.
- `r-x`: permisos del grupo.
- `r--`: permisos de otros.

### Valores numéricos

| Valor | Permiso |
|---|---|
| 4 | lectura |
| 2 | escritura |
| 1 | ejecución |
| 7 | lectura + escritura + ejecución |
| 5 | lectura + ejecución |

---

## 6. Usuarios y grupos

```bash
id usuario
groups usuario
sudo adduser usuario
sudo usermod -aG sudo usuario
sudo passwd usuario
sudo deluser usuario
sudo groupadd grupo
sudo usermod -aG grupo usuario
getent passwd
getent group
```

### Archivos importantes

| Archivo | Contenido |
|---|---|
| `/etc/passwd` | Usuarios del sistema |
| `/etc/shadow` | Contraseñas cifradas |
| `/etc/group` | Grupos |
| `/etc/sudoers` | Permisos de sudo |

Usar siempre `visudo` para editar sudoers:

```bash
sudo visudo
```

---

## 7. Procesos

```bash
ps aux
top
htop
pgrep nginx
pidof sshd
kill PID
kill -15 PID
kill -9 PID
nice
renice
```

### Señales frecuentes

| Señal | Uso |
|---|---|
| `SIGTERM` / `15` | Solicita terminar correctamente |
| `SIGKILL` / `9` | Fuerza cierre inmediato |
| `SIGHUP` / `1` | Recarga configuración en algunos servicios |

---

## 8. Servicios con systemd

```bash
systemctl status ssh
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl reload ssh
sudo systemctl enable ssh
sudo systemctl disable ssh
systemctl list-units --type=service
systemctl list-unit-files
```

### Ver logs de un servicio

```bash
journalctl -u ssh
journalctl -u ssh -f
journalctl -xe
```

---

## 9. Paquetes

### Debian/Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt install paquete
sudo apt remove paquete
sudo apt purge paquete
apt search paquete
apt show paquete
dpkg -l
```

### Red Hat/Fedora/Rocky/Alma

```bash
sudo dnf update
sudo dnf install paquete
sudo dnf remove paquete
dnf search paquete
dnf info paquete
rpm -qa
```

---

## 10. Discos y sistemas de archivos

```bash
lsblk
blkid
df -h
du -sh *
mount
findmnt
sudo fdisk -l
```

### Montaje temporal

```bash
sudo mount /dev/sdb1 /mnt
sudo umount /mnt
```

### Riesgo

Comandos como `mkfs`, `fdisk`, `parted` o `dd` pueden borrar datos. Usarlos solo si se entiende exactamente el dispositivo de destino.

---

## 11. Red básica en Linux

```bash
ip a
ip route
ip link
ss -tulnp
ping 8.8.8.8
traceroute google.com
dig google.com
nslookup google.com
curl -I https://example.com
```

---

## 12. Firewall básico

### UFW

```bash
sudo ufw status
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw deny 23/tcp
sudo ufw delete allow 80/tcp
```

### firewalld

```bash
sudo firewall-cmd --state
sudo firewall-cmd --list-all
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
```

---

## 13. Tareas programadas

### Cron

```bash
crontab -e
crontab -l
```

Ejemplo: ejecutar backup todos los días a las 02:00.

```cron
0 2 * * * /home/usuario/scripts/backup.sh
```

---

## 14. Checklist de diagnóstico rápido

```bash
hostnamectl
uptime
df -h
free -h
systemctl --failed
journalctl -p err -n 50
ip a
ip route
ss -tulnp
```

---

## 15. Mini script de mantenimiento

```bash
#!/bin/bash
set -euo pipefail

echo "== Sistema =="
hostnamectl

echo "== Disco =="
df -h

echo "== Memoria =="
free -h

echo "== Servicios fallidos =="
systemctl --failed || true

echo "== Últimos errores =="
journalctl -p err -n 20 --no-pager || true
```
