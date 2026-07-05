# 10 - Bases de datos para administración de sistemas

En administración de sistemas no basta con saber SQL. También hay que saber instalar, asegurar, hacer copias, restaurar, revisar logs y automatizar tareas del sistema gestor de bases de datos.

---

## 1. Conceptos esenciales

| Concepto | Explicación |
|---|---|
| SGBD | Sistema gestor de bases de datos |
| Base de datos | Conjunto organizado de datos |
| Tabla | Estructura formada por filas y columnas |
| Usuario | Cuenta que accede al SGBD |
| Rol | Conjunto de permisos |
| Backup lógico | Exportación SQL o formato portable |
| Backup físico | Copia de archivos internos del SGBD |
| Dump | Volcado de una base de datos |

---

## 2. SQL básico

```sql
CREATE DATABASE empresa;
USE empresa;
CREATE TABLE usuarios (
    id INT PRIMARY KEY,
    nombre VARCHAR(100),
    email VARCHAR(150)
);
INSERT INTO usuarios VALUES (1, 'Ana', 'ana@example.com');
SELECT * FROM usuarios;
UPDATE usuarios SET email = 'ana@empresa.local' WHERE id = 1;
DELETE FROM usuarios WHERE id = 1;
```

---

## 3. MySQL/MariaDB

### Servicio

```bash
sudo systemctl status mysql
sudo systemctl restart mysql
sudo journalctl -u mysql -n 50
```

### Acceso

```bash
mysql -u root -p
mysql -u usuario -p base_datos
```

### Usuarios y permisos

```sql
CREATE USER 'app'@'localhost' IDENTIFIED BY 'contraseña_segura';
GRANT SELECT, INSERT, UPDATE, DELETE ON empresa.* TO 'app'@'localhost';
FLUSH PRIVILEGES;
SHOW GRANTS FOR 'app'@'localhost';
```

### Backup

```bash
mysqldump -u root -p empresa > empresa.sql
mysqldump -u root -p --all-databases > todas.sql
```

### Restauración

```bash
mysql -u root -p empresa < empresa.sql
```

---

## 4. PostgreSQL

### Servicio

```bash
sudo systemctl status postgresql
sudo systemctl restart postgresql
sudo journalctl -u postgresql -n 50
```

### Acceso

```bash
sudo -u postgres psql
psql -U usuario -d base_datos
```

### Usuarios y bases

```sql
CREATE DATABASE empresa;
CREATE USER app WITH PASSWORD 'contraseña_segura';
GRANT CONNECT ON DATABASE empresa TO app;
```

### Backup

```bash
pg_dump empresa > empresa.sql
pg_dumpall > todas.sql
```

### Restauración

```bash
psql empresa < empresa.sql
```

---

## 5. SQLite

SQLite es una base de datos ligera basada en archivo.

```bash
sqlite3 app.db
```

```sql
.tables
.schema
SELECT * FROM tabla;
.backup backup.db
```

---

## 6. SQL Server desde PowerShell

En entornos Windows, SQL Server suele administrarse con herramientas gráficas, PowerShell y scripts SQL.

Comprobaciones generales:

```powershell
Get-Service | Where-Object {$_.Name -like '*SQL*'}
Get-EventLog -LogName Application -Newest 50 | Where-Object {$_.Source -like '*SQL*'}
```

---

## 7. Logs y diagnóstico

### Linux

```bash
journalctl -u mysql
journalctl -u mariadb
journalctl -u postgresql
```

### Comprobaciones comunes

- ¿El servicio está activo?
- ¿El puerto está escuchando?
- ¿El usuario tiene permisos?
- ¿La aplicación usa credenciales correctas?
- ¿Hay espacio en disco?
- ¿Existen errores en logs?

```bash
ss -tulnp | grep 3306
ss -tulnp | grep 5432
df -h
```

---

## 8. Automatizar backup MySQL

```bash
#!/bin/bash
set -euo pipefail

BD="empresa"
DESTINO="/backups/mysql"
FECHA=$(date +"%Y-%m-%d_%H-%M-%S")

mkdir -p "$DESTINO"
mysqldump "$BD" > "$DESTINO/${BD}_$FECHA.sql"
find "$DESTINO" -name "${BD}_*.sql" -mtime +7 -delete
```

---

## 9. Seguridad básica

- Usar usuarios específicos por aplicación.
- No usar root/admin desde aplicaciones.
- Limitar origen de conexión.
- Usar contraseñas fuertes.
- Proteger archivos de backup.
- No subir dumps con datos reales a repositorios públicos.
- Revisar permisos periódicamente.

---

## 10. Checklist de base de datos

- [ ] Servicio activo.
- [ ] Puerto correcto escuchando.
- [ ] Usuario específico creado.
- [ ] Permisos mínimos aplicados.
- [ ] Backup automatizado.
- [ ] Restauración probada.
- [ ] Logs revisables.
- [ ] Espacio en disco controlado.
- [ ] Credenciales protegidas.
