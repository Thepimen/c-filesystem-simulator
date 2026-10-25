# 💾 Inode-Based Filesystem Simulator in C

[![Language: C](https://img.shields.io/badge/Language-C99-00599C?style=flat-square&logo=c&logoColor=white)](https://en.cppreference.com/w/c)
[![POSIX](https://img.shields.io/badge/Standard-POSIX-black?style=flat-square&logo=linux)](https://pubs.opengroup.org/)
[![Systems Engineering](https://img.shields.io/badge/Domain-Operating_Systems-FF6F00?style=flat-square)](https://u-tad.com)

> **Simulador de Sistema de Archivos basado en Inodos:** Implementación modular en C de bajo nivel que emula la capa de almacenamiento, particionamiento de bloques, gestión de inodos y resolución de directorios típica de sistemas tipo UNIX.  
> *Desarrollado durante la etapa universitaria en Grado en Ingeniería del Software (U-tad, Sistemas Operativos / INSO).*

---

## 🏗️ Arquitectura de Almacenamiento

El simulador estructura un disco virtual particionado en bloques de datos contiguos:

- **Tamaño de bloque:** 512 bytes (`SIZE_BLOQUE 512`).
- **Capacidad de partición:** 100 bloques (`MAX_BLOQUES_PARTICION 100`).
- **Tabla de Inodos:** 24 inodos concurrentes (`MAX_INODOS 24`), con punteros directos a bloques de datos (`MAX_NUMS_BLOQUE_INODO 7`).
- **Bytemaps de Asignación:** Estructura de mapas de bits (bytemaps) para el seguimiento instantáneo de bloques libres y ocupados sin fragmentación externa.

---

## ⚙️ Operaciones del Sistema de Archivos

La consola interactiva permite ejecutar comandos de manipulación de bajo nivel:

| Comando | Función y Mecanismo Interno |
| :--- | :--- |
| `format` | Inicializa el superbloque, limpia la tabla de inodos y resetea el bytemap de bloques. |
| `dir` | Recorre los inodos activos e imprime metadatos (nombre, tamaño en bytes, bloques asignados). |
| `create` | Asigna un nuevo inodo libre y reserva bloques contiguos en el bytemap de datos. |
| `read` / `print` | Lee secuencialmente los buffers desde los bloques indexados por los punteros del inodo. |
| `write` / `copy` | Escribe contenido en la partición recalculando bloques necesarios y actualizando el inodo. |
| `rename` | Modifica de forma atómica el identificador del archivo en su inodo correspondiente. |
| `remove` | Libera los bloques asociados en el bytemap y marca el inodo como disponible (`0xFFFF`). |
| `bytemaps` | Vuelca en consola el mapa hexadecimal de asignación de bloques del disco virtual. |

---

## 🚀 Compilación y Ejecución

```bash
# Compilar con GCC habilitando advertencias estándar
gcc -Wall -Wextra -O2 SistemaOperativo.c -o filesystem_sim

# Ejecutar el simulador interactivo
./filesystem_sim
```

---

## 🎓 Contexto Académico

- **Centro:** U-tad (Centro Universitario de Tecnología y Arte Digital)
- **Grado:** Grado en Ingeniería del Software
- **Asignatura:** Sistemas Operativos (INSO)
- **Autores:** Luis Lázaro Pimentel & Miguel Torón
