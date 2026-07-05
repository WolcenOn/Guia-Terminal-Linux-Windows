# 19 - Integración con Script-Lab

Esta guía y Script-Lab deben complementarse sin duplicar funciones.

- Esta guía explica conceptos, comandos, procedimientos y buenas prácticas.
- Script-Lab puede almacenar scripts ejecutables, herramientas, laboratorios y proyectos prácticos.

---

## 1. Qué debe quedarse en esta guía

- Explicaciones pedagógicas.
- Tablas de comandos.
- Procedimientos paso a paso.
- Checklists.
- Runbooks.
- Plantillas de scripts en formato didáctico.
- Ejercicios.
- Buenas prácticas.

---

## 2. Qué debe ir a Script-Lab

- Scripts completos y ejecutables.
- Herramientas con parámetros.
- Generadores de scripts.
- Laboratorios prácticos.
- Proyectos con README propio.
- Pruebas de scripts.
- Ejemplos de automatización real.

---

## 3. Criterios para mover un script

Un script puede pasar a Script-Lab cuando cumple:

- Tiene objetivo claro.
- Tiene nombre descriptivo.
- Tiene parámetros documentados.
- Tiene control de errores.
- Genera salida clara.
- No contiene datos sensibles.
- Incluye ejemplo de uso.
- Ha sido probado en laboratorio.
- Tiene README o documentación mínima.

---

## 4. Estructura recomendada en Script-Lab

```text
Script-Lab/
├── README.md
├── bash/
│   ├── mantenimiento/
│   ├── backups/
│   ├── redes/
│   └── usuarios/
├── powershell/
│   ├── mantenimiento/
│   ├── inventario/
│   ├── eventos/
│   └── usuarios/
├── python/
│   ├── monitorizacion/
│   ├── informes/
│   ├── redes/
│   └── automatizacion/
└── labs/
    ├── linux-basico/
    ├── windows-basico/
    └── redes/
```

---

## 5. Plantilla README para cada script

```text
# Nombre del script

## Objetivo

Explica qué problema resuelve.

## Sistema compatible

Linux, Windows o multiplataforma.

## Requisitos

Herramientas, permisos y dependencias necesarias.

## Uso

Ejemplo de ejecución.

## Parámetros

Lista de parámetros aceptados.

## Salida esperada

Qué muestra o genera.

## Riesgos

Qué cambios realiza y cómo revertirlos.

## Pruebas

Cómo comprobar que funciona.
```

---

## 6. Flujo de trabajo recomendado

1. Explicar el concepto en esta guía.
2. Crear una plantilla didáctica.
3. Convertirla en script real en Script-Lab.
4. Probarlo en laboratorio.
5. Documentarlo.
6. Enlazarlo desde la guía.
7. Mejorarlo con versiones sucesivas.

---

## 7. Ejemplo de enlace cruzado

En esta guía:

```md
Para un ejemplo ejecutable, consulta Script-Lab: ruta/del/script.
```

En Script-Lab:

```md
Este script complementa la sección de backups de Guia-Terminal-Linux-Windows.
```

---

## 8. Roadmap inicial de scripts

- Inventario Linux.
- Inventario Windows.
- Comprobación de disco.
- Comprobación de servicios críticos.
- Backup con retención.
- Diagnóstico de red.
- Revisión de logs.
- Auditoría básica de usuarios.
- Generador de informe de mantenimiento.
