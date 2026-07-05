# Cheatsheet Linux

Referencia rápida de comandos Linux para administración.

---

## Sistema

```bash
hostnamectl
uname -a
cat /etc/os-release
uptime
whoami
id
```

## Archivos

```bash
pwd
ls -lah
cd /ruta
mkdir -p carpeta
cp origen destino
cp -r carpeta destino
mv origen destino
rm archivo
rm -r carpeta
find /ruta -name "*.log"
```

## Texto

```bash
cat archivo
less archivo
head archivo
tail archivo
tail -f archivo
grep "texto" archivo
grep -R "texto" /ruta
```

## Permisos

```bash
chmod 755 archivo
chmod +x script.sh
chown usuario:grupo archivo
ls -l
```

## Usuarios

```bash
sudo adduser usuario
sudo passwd usuario
sudo usermod -aG grupo usuario
id usuario
groups usuario
```

## Procesos

```bash
ps aux
top
htop
pgrep nombre
kill PID
kill -9 PID
```

## Servicios

```bash
systemctl status servicio
sudo systemctl start servicio
sudo systemctl stop servicio
sudo systemctl restart servicio
sudo systemctl enable servicio
journalctl -u servicio
```

## Red

```bash
ip a
ip route
ss -tulnp
ping 8.8.8.8
traceroute google.com
dig google.com
curl -I https://example.com
```

## Disco

```bash
lsblk
blkid
df -h
du -sh *
mount
findmnt
```

## Paquetes Debian/Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt install paquete
sudo apt remove paquete
apt search paquete
```

## Backups

```bash
tar -czf backup.tar.gz carpeta/
rsync -avh origen/ destino/
rsync -avh --dry-run origen/ destino/
```
