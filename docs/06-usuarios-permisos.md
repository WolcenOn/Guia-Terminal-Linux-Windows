# 06 - Usuarios y permisos

La gestión de usuarios y permisos es uno de los pilares de la administración de sistemas. Un mal permiso puede provocar fallos de servicio, pérdida de datos o problemas de seguridad.

---

## 1. Principio de mínimo privilegio

Un usuario, servicio o script debe tener solo los permisos necesarios para cumplir su función, y nada más.

Ejemplos:

- No usar `root` o administrador para tareas normales.
- No dar permisos `777` salvo en laboratorios controlados.
- No ejecutar servicios web con usuarios privilegiados.
- Separar usuarios humanos de usuarios de servicio.

---

## 2. Usuarios en Linux

```bash
whoami
id
id usuario
groups usuario
getent passwd
getent group
```

### Crear usuarios

```bash
sudo adduser usuario
sudo passwd usuario
```

### Modificar usuarios

```bash
sudo usermod -aG grupo usuario
sudo usermod -s /bin/bash usuario
sudo usermod -d /home/nuevo usuario
```

### Eliminar usuarios

```bash
sudo deluser usuario
sudo deluser --remove-home usuario
```

---

## 3. Grupos en Linux

```bash
sudo groupadd grupo
sudo groupdel grupo
sudo usermod -aG grupo usuario
groups usuario
```

### Ejemplo

```bash
sudo groupadd proyecto
sudo usermod -aG proyecto ana
sudo chown -R root:proyecto /srv/proyecto
sudo chmod -R 770 /srv/proyecto
```

---

## 4. Permisos Linux

```bash
ls -l archivo
chmod 644 archivo
chmod 755 script.sh
chmod +x script.sh
chown usuario:grupo archivo
chown -R usuario:grupo carpeta
```

### Permisos comunes

| Permiso | Uso típico |
|---|---|
| `600` | Archivo privado del usuario |
| `644` | Archivo legible por todos, editable por propietario |
| `700` | Carpeta o script privado |
| `755` | Script o carpeta accesible |
| `750` | Carpeta accesible por propietario y grupo |
| `770` | Carpeta colaborativa de grupo |

---

## 5. Permisos especiales Linux

| Permiso | Uso |
|---|---|
| SUID | Ejecutar con permisos del propietario |
| SGID | Heredar grupo o ejecutar con grupo |
| Sticky bit | Evita que usuarios borren archivos ajenos en carpetas compartidas |

```bash
chmod u+s binario
chmod g+s carpeta
chmod +t carpeta
```

Ejemplo típico:

```bash
ls -ld /tmp
```

---

## 6. sudo

```bash
sudo comando
sudo -l
sudo visudo
```

Nunca editar `/etc/sudoers` directamente con editores normales. Usar:

```bash
sudo visudo
```

Ejemplo de regla:

```text
usuario ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx
```

---

## 7. Usuarios en Windows

### CMD

```cmd
net user
net user usuario contraseña /add
net user usuario /delete
net localgroup
net localgroup administrators usuario /add
```

### PowerShell

```powershell
Get-LocalUser
New-LocalUser "usuario" -Password (Read-Host -AsSecureString)
Remove-LocalUser "usuario"
Get-LocalGroup
Add-LocalGroupMember -Group "Administrators" -Member "usuario"
Get-LocalGroupMember Administrators
```

---

## 8. Permisos NTFS

PowerShell permite revisar ACL:

```powershell
Get-Acl C:\Datos
```

Modificar ACL puede ser delicado. Una forma clásica es usar `icacls`:

```cmd
icacls C:\Datos
icacls C:\Datos /grant usuario:R
icacls C:\Datos /grant usuario:M
icacls C:\Datos /remove usuario
```

| Permiso | Significado |
|---|---|
| `R` | Read / lectura |
| `M` | Modify / modificar |
| `F` | Full control / control total |

---

## 9. Usuarios de servicio

Los servicios no deberían ejecutarse siempre como administrador/root.

Buenas prácticas:

- Crear un usuario específico por servicio importante.
- Dar acceso solo a sus carpetas necesarias.
- Evitar login interactivo si no hace falta.
- Documentar qué servicio usa cada usuario.

---

## 10. Auditoría básica

### Linux

```bash
last
lastlog
who
w
getent passwd
sudo grep sudo /var/log/auth.log
```

### Windows PowerShell

```powershell
Get-LocalUser
Get-LocalGroupMember Administrators
Get-WinEvent -LogName Security -MaxEvents 50
```

---

## 11. Script Bash: crear usuario básico

```bash
#!/bin/bash
set -euo pipefail

USUARIO="${1:-}"

if [ -z "$USUARIO" ]; then
    echo "Uso: $0 nombre_usuario"
    exit 1
fi

sudo adduser "$USUARIO"
echo "Usuario $USUARIO creado"
```

---

## 12. Script PowerShell: listar administradores locales

```powershell
$Grupo = "Administrators"
Get-LocalGroupMember -Group $Grupo | Select-Object Name, ObjectClass, PrincipalSource
```

---

## 13. Checklist de revisión de permisos

- [ ] ¿El usuario necesita realmente permisos elevados?
- [ ] ¿El grupo asignado es correcto?
- [ ] ¿La carpeta tiene permisos excesivos?
- [ ] ¿Hay usuarios antiguos que deben eliminarse?
- [ ] ¿Los servicios usan cuentas específicas?
- [ ] ¿Se han documentado cambios de permisos?
- [ ] ¿Se ha probado el acceso con usuario no administrador?
