# 20 - Active Directory y LDAP

Active Directory y LDAP son tecnologías fundamentales en administración de sistemas Windows y entornos mixtos. Permiten centralizar usuarios, grupos, equipos, permisos y políticas.

---

## 1. Conceptos básicos

| Concepto | Explicación |
|---|---|
| Directorio | Base de datos jerárquica de objetos |
| Dominio | Unidad lógica de administración |
| Controlador de dominio | Servidor que autentica y gestiona el dominio |
| Usuario | Cuenta de persona o servicio |
| Grupo | Conjunto de usuarios o equipos |
| OU | Unidad organizativa para ordenar objetos |
| GPO | Directiva de grupo aplicada a usuarios o equipos |
| LDAP | Protocolo para consultar y modificar directorios |
| Kerberos | Protocolo de autenticación habitual en dominios Windows |
| DNS | Servicio crítico para localizar controladores de dominio |

---

## 2. Para qué se usa

- Centralizar usuarios.
- Gestionar grupos y permisos.
- Aplicar políticas de seguridad.
- Administrar equipos unidos al dominio.
- Controlar acceso a recursos compartidos.
- Auditar inicios de sesión.
- Automatizar altas, bajas y cambios.

---

## 3. Estructura lógica

```text
Dominio
├── Usuarios
├── Grupos
├── Equipos
├── Unidades organizativas
└── Políticas de grupo
```

Ejemplo:

```text
empresa.local
├── OU=Usuarios
├── OU=Equipos
├── OU=Servidores
└── OU=Departamentos
    ├── OU=Administracion
    ├── OU=Sistemas
    └── OU=Desarrollo
```

---

## 4. Comprobaciones básicas en Windows

```powershell
whoami
hostname
ipconfig /all
nltest /dsgetdc:dominio.local
gpresult /r
```

Comprobar dominio del equipo:

```powershell
(Get-CimInstance Win32_ComputerSystem).Domain
```

---

## 5. PowerShell y Active Directory

En entornos con el módulo de Active Directory instalado:

```powershell
Get-ADDomain
Get-ADUser -Filter *
Get-ADGroup -Filter *
Get-ADComputer -Filter *
```

Consultar un usuario:

```powershell
Get-ADUser usuario -Properties *
```

Consultar miembros de un grupo:

```powershell
Get-ADGroupMember "NombreGrupo"
```

---

## 6. Usuarios

Crear usuario de forma controlada requiere definir nombre, ubicación, contraseña, grupos y política.

Ejemplo conceptual:

```powershell
New-ADUser -Name "Ana Perez" -SamAccountName "aperez" -UserPrincipalName "aperez@empresa.local" -Enabled $true
```

Operaciones habituales:

```powershell
Enable-ADAccount usuario
Disable-ADAccount usuario
Unlock-ADAccount usuario
Set-ADAccountPassword usuario
```

---

## 7. Grupos

Los grupos facilitan asignar permisos sin gestionar usuario por usuario.

Buenas prácticas:

- Asignar permisos a grupos, no a usuarios individuales.
- Usar nombres claros.
- Documentar propósito del grupo.
- Revisar miembros periódicamente.

Comandos:

```powershell
Get-ADGroup -Filter *
Get-ADGroupMember "Grupo"
Add-ADGroupMember "Grupo" usuario
Remove-ADGroupMember "Grupo" usuario
```

---

## 8. Unidades organizativas

Las OU sirven para ordenar objetos y aplicar políticas.

```powershell
Get-ADOrganizationalUnit -Filter *
```

Ejemplo conceptual:

```powershell
New-ADOrganizationalUnit -Name "Sistemas" -Path "DC=empresa,DC=local"
```

---

## 9. Políticas de grupo

Las GPO permiten aplicar configuraciones a usuarios y equipos.

Ejemplos de uso:

- Políticas de contraseña.
- Bloqueo de pantalla.
- Restricciones de software.
- Configuración de firewall.
- Scripts de inicio o cierre.
- Mapeo de unidades de red.

Comandos útiles:

```cmd
gpupdate /force
gpresult /r
gpresult /h informe.html
```

---

## 10. LDAP

LDAP permite consultar directorios mediante rutas llamadas DN.

Ejemplo de DN:

```text
CN=Ana Perez,OU=Usuarios,DC=empresa,DC=local
```

Componentes:

| Parte | Significado |
|---|---|
| `CN` | Common Name |
| `OU` | Organizational Unit |
| `DC` | Domain Component |

---

## 11. Diagnóstico básico de dominio

Revisar:

- DNS correcto.
- Conectividad con controlador de dominio.
- Hora sincronizada.
- Equipo unido al dominio.
- Políticas aplicadas.
- Permisos de usuario.

Comandos:

```cmd
ipconfig /all
nslookup dominio.local
nltest /dsgetdc:dominio.local
gpresult /r
w32tm /query /status
```

---

## 12. Buenas prácticas

- No usar cuentas compartidas.
- Separar cuentas de usuario y cuentas administrativas.
- Aplicar mínimo privilegio.
- Usar grupos para permisos.
- Documentar OU y grupos.
- Revisar miembros de grupos privilegiados.
- Deshabilitar cuentas que ya no se usan.
- Auditar cambios relevantes.
- Mantener DNS correctamente configurado.

---

## 13. Checklist AD/LDAP

- [ ] DNS del cliente apunta al dominio.
- [ ] Equipo unido correctamente al dominio.
- [ ] Hora sincronizada.
- [ ] Usuarios organizados en OU.
- [ ] Grupos documentados.
- [ ] Permisos asignados a grupos.
- [ ] GPO aplicadas y verificadas.
- [ ] Cuentas antiguas revisadas.
- [ ] Administradores auditados.
- [ ] Procedimientos de alta y baja documentados.
