# Script-Lab: laboratorio práctico

Script-Lab es la aplicación web complementaria donde se realizan las prácticas de esta guía.

- Guía web: teoría, explicación, búsqueda rápida, casos y retos.
- Script-Lab: aplicación para practicar, generar bloques, preparar entregas y recibir feedback.
- Repositorio de Script-Lab: código fuente, laboratorios y documentación del laboratorio.

---

## Entrar a la aplicación

!!! success "Abrir Script-Lab"

    [Ir a la aplicación web de Script-Lab](https://wolcenon.github.io/Script-Lab/)

Repositorio público:

[Ver repositorio de Script-Lab](https://github.com/WolcenOn/Script-Lab)

---

## Carga segura desde la guía

La guía puede abrir Script-Lab directamente en un ejercicio usando un identificador seguro:

```text
https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-04-REDES
```

Script-Lab solo carga IDs válidos y existentes en su lista blanca de ejercicios. Si recibe un ID desconocido, no carga contenido externo y vuelve a un ejercicio por defecto.

---

## Integración profunda

El flujo previsto es:

```text
Ejercicio de la guía -> Script-Lab -> Blockly -> Código -> Feedback -> Entrega -> Rama -> Pull Request
```

Cada ejercicio tiene:

- ID propio.
- Carga directa por URL.
- Bloques iniciales.
- Rama sugerida.
- Entregables.
- Criterios de feedback.

---

## Abrir ejercicios directamente en Script-Lab

| Nivel | Ejercicio | Abrir en Script-Lab | Lab en repositorio |
|---|---|---|---|
| 1 | Terminal básica | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-01-TERMINAL) | [Lab 01](https://github.com/WolcenOn/Script-Lab/blob/main/labs/01-terminal-basica/README.md) |
| 2 | Linux administración | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-02-LINUX) | [Lab 02](https://github.com/WolcenOn/Script-Lab/blob/main/labs/02-linux-administracion/README.md) |
| 3 | Windows PowerShell | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-03-WINDOWS) | [Lab 03](https://github.com/WolcenOn/Script-Lab/blob/main/labs/03-windows-powershell/README.md) |
| 4 | Redes | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-04-REDES) | [Lab 04](https://github.com/WolcenOn/Script-Lab/blob/main/labs/04-redes/README.md) |
| 5 | Backups | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-05-BACKUPS) | [Lab 05](https://github.com/WolcenOn/Script-Lab/blob/main/labs/05-backups/README.md) |
| 6 | Scripting | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-06-SCRIPTING) | [Lab 06](https://github.com/WolcenOn/Script-Lab/blob/main/labs/06-scripting/README.md) |
| 7 | Proyecto final | [Abrir ejercicio](https://wolcenon.github.io/Script-Lab/?exercise=GT-LAB-07-PROYECTO) | [Lab 07](https://github.com/WolcenOn/Script-Lab/blob/main/labs/07-proyecto-final/README.md) |

---

## Cómo usarlo con la guía

!!! tip "Flujo recomendado"

    1. Estudia el tema en esta web.
    2. Pulsa "Abrir ejercicio".
    3. Script-Lab carga el ejercicio por ID validado.
    4. Ajusta los bloques Blockly.
    5. Compara el código generado en Bash, PowerShell o Python.
    6. Escribe comandos, pseudocódigo o explicación.
    7. Revisa feedback y criterios pendientes.
    8. Copia la entrega sugerida.
    9. Crea una rama de trabajo y abre una Pull Request.

---

## Dinámica de ramas y feedback

Formato de rama recomendado:

```text
lab/<id-ejercicio>/<nombre>
```

Ejemplo:

```text
lab/gt-lab-04-redes/ana
```

El feedback debe revisar:

- Comprensión del problema.
- Orden de diagnóstico.
- Uso de comandos o bloques.
- Evidencias.
- Conclusiones.
- Mejora propuesta.

---

## Interfaz integrada

La interfaz principal de Script-Lab permite:

1. Cargar ejercicios desde URL segura.
2. Seleccionar ejercicio manualmente.
3. Generar bloques visuales iniciales.
4. Generar código en Bash, PowerShell o Python.
5. Escribir comandos, pseudocódigo o explicación.
6. Detectar criterios cubiertos y pendientes.
7. Mostrar feedback inmediato.
8. Exportar entrega en Markdown.

---

## Siguiente paso

[Entrar ahora a Script-Lab](https://wolcenon.github.io/Script-Lab/)
