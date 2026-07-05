# 18 - Ansible e infraestructura como código

La infraestructura como código consiste en describir sistemas, configuraciones y despliegues mediante archivos versionados. Así se reducen errores manuales, se facilita la repetición y se documenta el estado deseado de la infraestructura.

---

## 1. Qué es Ansible

Ansible es una herramienta de automatización que permite administrar sistemas de forma declarativa. Se usa para instalar paquetes, copiar archivos, configurar servicios, gestionar usuarios y aplicar cambios repetibles en varios equipos.

---

## 2. Conceptos básicos

| Concepto | Explicación |
|---|---|
| Inventario | Lista de equipos gestionados |
| Playbook | Archivo con tareas a ejecutar |
| Módulo | Unidad de acción de Ansible |
| Task | Tarea concreta dentro de un playbook |
| Handler | Acción que se ejecuta cuando una tarea notifica un cambio |
| Role | Estructura reutilizable de automatización |
| Idempotencia | Ejecutar varias veces sin romper el sistema ni repetir cambios innecesarios |

---

## 3. Inventario básico

```ini
[servidores]
servidor1 ansible_host=192.168.1.10
servidor2 ansible_host=192.168.1.11

[linux]
servidor1
servidor2
```

---

## 4. Comandos básicos

```bash
ansible --version
ansible all -i inventario.ini -m ping
ansible servidores -i inventario.ini -m setup
ansible-playbook -i inventario.ini playbook.yml
```

---

## 5. Playbook básico

```yaml
- name: Comprobacion basica de servidores
  hosts: servidores
  become: true
  tasks:
    - name: Instalar paquete curl
      ansible.builtin.package:
        name: curl
        state: present

    - name: Asegurar servicio activo
      ansible.builtin.service:
        name: ssh
        state: started
        enabled: true
```

---

## 6. Estructura recomendada

```text
ansible/
├── inventario.ini
├── playbooks/
│   ├── mantenimiento.yml
│   ├── usuarios.yml
│   └── servicios.yml
└── roles/
    └── servidor_base/
        ├── tasks/
        ├── handlers/
        ├── templates/
        └── files/
```

---

## 7. Casos de uso en administración de sistemas

- Instalar paquetes comunes.
- Crear usuarios.
- Copiar archivos de configuración.
- Reiniciar servicios cuando cambia una configuración.
- Aplicar hardening básico.
- Ejecutar comprobaciones periódicas.
- Desplegar configuraciones en varios servidores.

---

## 8. Buenas prácticas

- Versionar playbooks con Git.
- Probar en laboratorio antes de producción.
- Evitar cambios manuales no documentados.
- Usar variables para valores que cambian.
- Separar inventario, playbooks y roles.
- Documentar requisitos.
- Ejecutar primero en un grupo pequeño.
- Revisar cambios antes de aplicarlos masivamente.

---

## 9. Relación con esta guía

Esta guía enseña comandos y conceptos. Ansible permite convertir esos comandos en automatización repetible.

Ejemplo de evolución:

```text
Comando manual -> script -> playbook -> rol reutilizable -> procedimiento profesional
```

---

## 10. Checklist Ansible

- [ ] Inventario documentado.
- [ ] Conectividad comprobada.
- [ ] Playbook probado en laboratorio.
- [ ] Variables separadas.
- [ ] Cambios versionados.
- [ ] Resultado verificado.
- [ ] Rollback o recuperación documentada.
