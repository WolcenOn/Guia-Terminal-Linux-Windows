# 00 - Hoja de ruta de la guía

Esta hoja de ruta sirve para que la guía crezca de forma ordenada y no se quede ningún bloque importante fuera. Está orientada a cubrir una base equivalente a ASIR y extenderla hacia un nivel profesional.

---

## 1. Base de terminal

Antes de aprender comandos sueltos, hay que entender cómo funciona una terminal.

### Objetivos

- Saber moverse por el sistema de archivos.
- Entender rutas absolutas y relativas.
- Usar argumentos, opciones y parámetros.
- Encadenar comandos.
- Redirigir entrada, salida y errores.
- Consultar ayuda y documentación.

### Temas

- Terminal, shell y consola.
- Diferencias entre Bash, CMD y PowerShell.
- Prompt, usuario actual y directorio actual.
- Comandos internos y externos.
- Variables de entorno.
- Comodines: `*`, `?`, rangos y patrones.
- Redirecciones: `>`, `>>`, `<`, `2>`, `2>&1`.
- Tuberías: `|`.
- Códigos de salida.

---

## 2. Administración de sistemas operativos

Este bloque cubre la administración diaria de sistemas Linux y Windows.

### Linux

- Estructura de directorios.
- Gestión de paquetes.
- Usuarios, grupos y permisos.
- Procesos y señales.
- Servicios con `systemd`.
- Logs con `journalctl` y `/var/log`.
- Discos, particiones y sistemas de archivos.
- Copias de seguridad.
- Tareas programadas con `cron` y timers de systemd.

### Windows

- CMD y PowerShell.
- Usuarios y grupos locales.
- Servicios.
- Registro de eventos.
- Programador de tareas.
- Permisos NTFS.
- Administración remota.
- Inventario del sistema.

---

## 3. Redes y servicios

La administración de sistemas necesita una buena base de redes.

### Temas

- IPv4, IPv6, máscaras y puertas de enlace.
- DNS, DHCP, NAT y routing básico.
- Diagnóstico de conectividad.
- Puertos y sockets.
- Firewall en Linux y Windows.
- SSH.
- HTTP/HTTPS.
- FTP/SFTP.
- Correo: SMTP, IMAP y POP3.
- Compartición de archivos: SMB/NFS.
- Monitorización de servicios.

---

## 4. Scripting

El scripting permite pasar de ejecutar comandos manuales a automatizar procesos repetibles.

### Lenguajes principales

| Lenguaje | Uso recomendado |
|---|---|
| Bash | Automatización en Linux, servidores y scripts de mantenimiento |
| PowerShell | Administración de Windows, Microsoft 365, Active Directory y automatización de objetos |
| Python | Automatización multiplataforma, análisis de logs, APIs, informes y herramientas propias |

### Conceptos obligatorios

- Variables.
- Condicionales.
- Bucles.
- Funciones.
- Parámetros.
- Validación de entrada.
- Gestión de errores.
- Logs.
- Ficheros de configuración.
- Salida legible y salida para máquinas.
- Modo seguro o `dry-run`.

---

## 5. Bases de datos

En ASIR se trabaja tanto la gestión de bases de datos como la administración de sistemas gestores.

### Temas

- SQL básico y avanzado.
- Usuarios, permisos y roles.
- Backups y restauración.
- Importación y exportación.
- Optimización básica.
- Logs del SGBD.
- Automatización de copias.
- Monitorización.

### Herramientas frecuentes

- MySQL/MariaDB.
- PostgreSQL.
- SQLite.
- SQL Server.

---

## 6. Aplicaciones web y servicios de Internet

La guía debe cubrir la implantación y mantenimiento de aplicaciones web.

### Temas

- Servidores web: Apache, Nginx e IIS.
- PHP, Python y runtimes de aplicaciones.
- Virtual hosts.
- Certificados TLS.
- Logs web.
- Reverse proxy.
- Despliegue de CMS.
- Variables de entorno.
- Permisos de directorios web.
- Automatización de despliegues.

---

## 7. Seguridad y alta disponibilidad

La seguridad no debe quedar como un añadido final. Tiene que estar presente en todos los bloques.

### Temas

- Principio de mínimo privilegio.
- Hardening de sistemas.
- Firewall.
- Actualizaciones.
- Auditoría de usuarios.
- Copias y recuperación.
- Cifrado.
- SSH seguro.
- Gestión de secretos.
- Alta disponibilidad básica.
- Balanceo y tolerancia a fallos.
- Monitorización y alertas.

---

## 8. Nivel profesional

Una vez cubierta la base ASIR, la guía debe avanzar hacia herramientas y prácticas profesionales.

### Temas

- Git y GitHub.
- Docker y Docker Compose.
- CI/CD básico.
- Infraestructura como código.
- Ansible.
- Monitorización con Prometheus/Grafana o alternativas.
- Centralización de logs.
- Documentación técnica.
- Runbooks.
- Procedimientos de cambio.
- Automatización segura.

---

## 9. Criterio para añadir nuevos contenidos

Cada nuevo tema debería tener:

1. Explicación clara.
2. Tabla de comandos principales.
3. Ejemplos comentados.
4. Casos de uso reales.
5. Errores comunes.
6. Ejemplo de automatización.
7. Checklist de verificación.

---

## 10. Relación con Script-Lab

Esta guía explica comandos, conceptos y procedimientos. Script-Lab puede usarse como laboratorio para scripts completos:

- Scripts de backup.
- Scripts de inventario.
- Scripts de monitorización.
- Scripts de despliegue.
- Scripts de auditoría.
- Generadores de scripts.
