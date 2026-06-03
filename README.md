# Trabajo Practico Final - Testeo y Prueba de Software
---
## Sistema de turnos - Salita Odontologica
---
**Institución:** Universidad de Belgrano
**Materia:** Testeo y Prueba de Software
**Alumno:** Sergio Jesus Apollonio
**Año:** 2025
---
1. [Objetivo del Software](#1-objetivo-del-software)
2. [Requerimientos Funcionales](#2-requerimientos-funcionales)
3. [Requerimientos No Funcionales](#3-requerimientos-no-funcionales)
4. [Entidades del Sistema](#4-entidades-del-sistema)
5. [Arquitectura del Sistema](#5-arquitectura-del-sistema)
6. [Diagramas UML](#6-diagramas-uml)
   - [Diagrama de Clases](#61-diagrama-de-clases)
   - [Diagrama de Casos de Uso](#62-diagrama-de-casos-de-uso)
   - [Secuencia: Registrar Préstamo](#63-secuencia-registrar-préstamo)
   - [Secuencia: Registrar Devolución](#64-secuencia-registrar-devolución)
7. [Suite de Tests](#7-suite-de-tests)
8. [Ejecución de las Pruebas](#8-ejecución-de-las-pruebas)
   - [Plan de Ejecución](#81-plan-de-ejecución)
   - [Resultados](#82-resultados)
   - [Cobertura de Código](#83-cobertura-de-código)
9. [Pruebas End-to-End (E2E)](#10-pruebas-end-to-end-e2e)
   - [Descripción y Enfoque](#101-descripción-y-enfoque)
   - [Plan de Ejecución E2E](#102-plan-de-ejecución-e2e)
   - [Escenarios](#103-escenarios)
   - [Resultados E2E](#104-resultados)
10. [Cómo Ejecutar](#9-cómo-ejecutar)
---
## 1. Objetivo del Software
El propósito principal de este software es optimizar el flujo de trabajo operativo de un consultorio odontológico mediante la automatización y el control estricto de la agenda de citas médicas. El sistema mitiga problemas tradicionales como la sobreposición horaria (coincidencia de dos pacientes en un mismo bloque), la pérdida de registros de contacto de pacientes y la falta de orden cronológico. Ofrece una base sólida e íntegra sobre la cual el personal administrativo puede dar de alta pacientes, reservar turnos y liberar espacios en la agenda de forma ágil y determinista.

---

## 2. Requerimientos del Sistema

### 2.1. Requerimientos Funcionales (RF)
* **RF-01 Gestión de Pacientes:** El sistema debe registrar de forma obligatoria el nombre y teléfono de contacto de cada paciente.
* **RF-02 Control de Disponibilidad:** El software debe verificar e impedir de forma mandatoria la asignación de dos turnos en el mismo horario exacto dentro del consultorio.
* **RF-03 Cronología Automática:** La agenda de turnos debe listarse siempre de manera ordenada, mostrando primero las citas más próximas cronológicamente.
* **RF-04 Cancelación Eficiente:** El sistema debe permitir remover turnos de la agenda realizando búsquedas indexadas por el nombre del paciente, sin importar mayúsculas o minúsculas.

### 2.2. Requerimientos No Funcionales (RNF)
* **RNF-01 Precisión Temporal:** El manejo del tiempo debe realizarse utilizando tipos de datos nativos avanzados de Python (`datetime`), asegurando que las validaciones de tiempo sean inmunes a formatos de texto inconsistentes.
* **RNF-02 Complejidad Algorítmica:** El algoritmo de ordenación de turnos debe responder eficientemente, utilizando un enfoque de ordenamiento con una complejidad temporal óptima de $O(n \log n)$.
* **RNF-03 Modularidad del Código:** El sistema debe estructurarse bajo separación estricta de responsabilidades, aislando los modelos de datos de la lógica de control.

---

## 3. Entidades del Sistema
El dominio del problema está definido por las siguientes tres estructuras de datos interconectadas:

| Entidad | Atributo | Tipo de Dato | Descripción / Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| **Paciente** | nombre <br> telefono | `str` <br> `str` | Nombre completo del paciente.<br>Teléfono de contacto directo. |
| **Turno** | paciente <br> fecha_hora <br> motivo | `Paciente` <br> `datetime` <br> `str` | Instancia vinculada al paciente.<br>Fecha y hora de la cita (Única).<br>Descripción médica (ej: "Endodoncia"). |
| **Consultorio** | nombre <br> lista_turnos | `str` <br> `list[Turno]` | Nombre de la clínica dental.<br>Colección indexada de citas vigentes. |

---

## 4. Arquitectura del Sistema
El software está estructurado bajo un patrón monolítico modular de tres capas lógicas:
1. **Capa de Dominio (Modelos):** Clases puras (`Paciente` y `Turno`) encargadas exclusivamente de representar los datos de negocio y su estructura básica.
2. **Capa de Aplicación (Lógica del Negocio):** Centralizada en la clase `Consultorio`. Aquí residen las validaciones complejas, el control de colisiones horarias y la mutación segura del estado de la agenda de citas.
3. **Capa de Presentación:** Bloque ejecutable principal (`__main__`) que simula la interacción de la consola, enviando las órdenes e imprimiendo los resultados en la terminal del operador.

---

## 5. Diagramas UML (Especificaciones Conceptuales)

### 5.1. Diagrama de Clases
Muestra las relaciones estáticas del sistema: un `Consultorio` posee y administra una lista de composición de muchos (`*`) `Turnos`, y cada `Turno` tiene asociado de forma obligatoria un (`1`) `Paciente`.

```text
+---------------------------------------+
|               Consultorio             |
+---------------------------------------+
| - nombre: str                         |
| - lista_turnos: list[Turno]           |
+---------------------------------------+
| + agendar_turno(p, fh, m): bool       |
| + mostrar_turnos(): void              |
| + cancelar_turno(nombre_p): bool      |
+---------------------------------------+
                   | 1
                   |
                   | *
+---------------------------------------+
|                  Turno                |
+---------------------------------------+
| - paciente: Paciente                  |
| - fecha_hora: datetime                |
| - motivo: str                         |
+---------------------------------------+
                   | 1
                   |
                   | 1
+---------------------------------------+
|                Paciente               |
+---------------------------------------+
| - nombre: str                         |
| - telefono: str                       |
+---------------------------------------+

